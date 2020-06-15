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
    <button @click="countWords()" @enter="countWords()">Count</button>
  </div>
</template>

<script>
export default {
  name: "BoxWord",
  data() {
    return {
      text: "",
      words: [],
      i: 0,
      frequencyWord: {}
    };
  },
  methods: {
    splitWords() {
      this.words = this.text
        .split(/[^A-ZÀ-ź]/gi)
        .filter(item => item != "")
        .sort();
    },
    countWords() {
      this.splitWords();
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
