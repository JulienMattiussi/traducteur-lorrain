<template>
  <h1 class="title">
    Le Traducteur Lorrain
    <i
      >(using
      <a href="https://www.npmjs.com/package/lorrainjs" target="lorrainjs"
        >lorrainjs</a
      >)</i
    >
  </h1>
  <img
    alt="Lorraine logo"
    class="logo"
    src="./assets/Blason_Lorraine.svg.png"
  />
  <TranslatePanel />
</template>

<script>
import TranslatePanel from "./components/TranslatePanel.vue";

export default {
  name: "App",
  components: {
    TranslatePanel,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
  font-size: large;
}

.logo {
  width: 50px;
}
.title {
  color: red;
}

i {
  font-size: small;
  color: black;
}

a:visited {
  color: inherit;
}
</style>
