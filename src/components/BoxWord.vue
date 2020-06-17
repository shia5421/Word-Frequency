<template>
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

    <table v-if="this.words.length > 0">
      <tr>
        <th>Words</th>
        <th>Rank</th>
      </tr>

      <tr v-for="{ name, number } in this.frequencyWord" :key="name.id">
        <td>{{ name }}</td>
        <td>{{ number }}</td>
      </tr>
    </table>
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
      i: 0,
    };
  },
  methods: {
    splitWords() {
      this.words = this.text
        .split(/[^A-ZÀ-ź]/gi)
        .filter((item) => item != "")
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
        number: 1,
      };

      this.words.reduce((previousItem, actualItem) => {
        if (previousItem === actualItem) {
          this.frequencyWord[this.i - 1].number++;
          return previousItem;
        } else {
          this.frequencyWord[this.i] = {
            name: actualItem,
            number: 1,
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
    },
  },
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
table {
  margin: 0 auto;
  padding: 0rem 0.5rem;
  text-align: left;
  border: solid;
  border-radius: 5px;
  width: 90%;
}

@media only screen and (max-width: 787px) {
  #box_word {
    max-width: 380px;
  }
  table {
    max-width: 100%;
    width: 50%;
  }
}
</style>
