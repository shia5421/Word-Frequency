<template>
  <div>
    <div id="box_word">
      <textarea
        name="wordCounter"
        id="wordCounter"
        cols="30"
        rows="10"
        placeholder="Write here ;)"
        v-model="text"
        maxlength="2048"
      ></textarea>

      <div class="optionButtons">
        <select v-model="order" @click="orderWords()">
          <option disabled value>Select Order</option>
          <option>Ascending</option>
          <option>Descending</option>
          <option>Alphabetic</option>
        </select>
        <button @click="count()">Count Words</button>
      </div>
    </div>
    <div>
      <table v-if="this.words.length > 0" class="content-table">
        <thead>
          <tr>
            <th>Words</th>
            <th width="50px">Rank</th>
          </tr>
        </thead>

        <tbody>
          <tr v-for="{ name, number } in this.frequencyWord" :key="name.id">
            <td>{{ name }}</td>
            <td class="amount">{{ number }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "BoxWord",
  data() {
    return {
      text: "",
      words: [],
      frequencyWord: [],
      order: "",
      i: 0
    };
  },
  methods: {
    splitWords() {
      this.words = this.text
        .toLowerCase()
        .split(/[^A-ZÀ-ź]/gi)
        .filter(item => item != "")
        .sort();
    },
    orderWords() {
      switch (this.order) {
        case "Ascending":
          this.frequencyWord.sort((a, b) => a.number - b.number);
          break;
        case "Descending":
          this.frequencyWord.sort((a, b) => b.number - a.number);
          break;
        case "Alphabetic":
          this.frequencyWord.sort((a, b) => (a.name > b.name ? 1 : -1));
          break;
        default:
          this.frequencyWord.sort((a, b) => b.number - a.number);
      }
    },
    countWords() {
      this.frequencyWord = [];
      this.i = 1;

      this.frequencyWord[0] = {
        name: this.words[0],
        number: 1
      };

      this.words.reduce((previousItem, actualItem) => {
        if (previousItem === actualItem) {
          this.frequencyWord[this.i - 1].number++;
          return previousItem;
        } else {
          this.frequencyWord[this.i] = {
            name: actualItem,
            number: 1
          };
          this.i++;
          return actualItem;
        }
      });
    },
    count() {
      this.splitWords();
      this.countWords();
      this.orderWords();
    }
  }
};
</script>

<style scoped>
#box_word {
  display: flex;
  flex-direction: column;
  margin: 0 auto;
  max-width: 530px;
}
textarea {
  padding: 0.5rem 0.5rem;
  flex: 1;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  border-radius: 0px 4px 4px 4px;
  resize: none;
  outline: none;
  font-size: 1rem;
  box-shadow: 0px 3px 4px rgba(0, 0, 0, 0.1);
}
.optionButtons {
  display: flex;
  justify-content: space-between;
  margin-top: 0.5rem;
  margin-bottom: 1rem;
}
.optionButtons select {
  cursor: pointer;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 0 2px rgb(204, 204, 204);
  font-size: 0.875rem;
  color: #474747;
  text-align: left;
  padding: 0rem 0.5rem;
  outline: none;
}
.optionButtons button {
  height: 2rem;
  padding: 0rem 0.5rem;
  border: none;
  border-radius: 4px;
  background: #303030;
  color: white;
  font-size: 1rem;
  font-weight: bold;
  box-shadow: 0px 3px 4px rgba(0, 0, 0, 0.4);
  cursor: pointer;
  outline: none;
}
.optionButtons button:active {
  background: #707070;
}

.content-table {
  margin: 0 auto;
  border-collapse: collapse;
  text-align: left;
  min-width: 530px;
  animation: dropDown 2s forwards;
}
.content-table thead tr {
  background: #303030;
  color: #ffffff;
  font-weight: bold;
}
.content-table th,
.content-table td {
  padding: 12px 15px;
}
.content-table tbody tr {
  border-bottom: 1px solid #dddddd;
}
.amount {
  text-align: center;
}
@keyframes dropDown {
  from {
    opacity: 0;
    transform: translate3d(0, -30px, 0);
  }
  to {
    opacity: 1;
    transform: translate3d(0, 0, 0);
  }
}
@media only screen and (max-width: 787px) {
  #box_word {
    max-width: 380px;
  }
  .content-table {
    min-width: 380px;
  }
}
</style>
