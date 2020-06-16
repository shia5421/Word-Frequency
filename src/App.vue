<template>
  <div id="app">
    <h1>Words Frequency</h1>
    <BoxWord />
  </div>
</template>

<script>
import BoxWord from "./components/BoxWord.vue";

export default {
  name: "App",
  components: {
    BoxWord
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0px;
  padding: 0px;
}
h1 {
  font-size: 3.75rem;
  margin-bottom: 1.5rem;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000000;
  margin-top: 3.75rem;
}
</style>
