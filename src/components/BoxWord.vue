<template>
  <div class="box_word">
    <textarea
      name="wordCounter"
      id="wordCounter"
      cols="30"
      rows="10"
      placeholder="Write here ;)"
      v-model="text"
    ></textarea>
    <div>
      <button @click="count()">Count</button>
      <select v-model="order" @click="orderWords()">
        <option disabled value>Select Order</option>
        <option>Ascending</option>
        <option>Descending</option>
        <option>Alphabetic</option>
      </select>
    </div>
    <div v-for="{name,number} in this.frequencyWord" :key="name.id">
      <p>{{name}}</p>
      <p>{{number}}</p>
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
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
