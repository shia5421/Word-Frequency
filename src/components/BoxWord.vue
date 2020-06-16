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
    <button @click="countWords()">Count</button>
    <button @click="alphabeticalOrder()">alphabeticalOrder</button>
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
    decreasingOrder() {
      this.frequencyWord.sort((a, b) => b.number - a.number);
    },
    alphabeticalOrder() {
      this.frequencyWord.sort((a, b) => (a.name > b.name ? 1 : -1));
    },
    countWords() {
      this.splitWords();

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

      this.decreasingOrder();
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
