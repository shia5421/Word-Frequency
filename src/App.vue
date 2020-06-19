<template>
  <div id="app">
    <header>
      <h1>Words Frequency</h1>
    </header>
    <main>
      <BoxWord />
    </main>
    <footer>
      <a href="https://github.com/rafaelofil/Word-Frequency" target="_blank">
        <img id="img-github" src="./assets/img/github.jpg" alt="GitHub" />
      </a>
      <p>
        Made by
        <a href="https://github.com/rafaelofil">Rafael Filho</a>
      </p>
    </footer>
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
  font-size: 4.5rem;
  margin-bottom: 1.5rem;
}
main {
  min-height: calc(100vh - 420px);
}
footer a {
  font-weight: bold;
  color: #548ba1;
  outline: none;
  text-decoration: none;
}
footer a:hover {
  color: #000000;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000000;
  margin-top: 3.75rem;
  animation: fadeIn 2s forwards;
}
#img-github {
  width: 212px;
  height: 212px;
  margin-top: 0.5rem;
  scroll-behavior: smooth 2s;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@media only screen and (max-width: 787px) {
  h1 {
    font-size: 3rem;
  }
  main {
    min-height: calc(100vh - 390px);
  }
}
</style>
