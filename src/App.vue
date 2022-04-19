<template>
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
}

.logo {
  width: 50px;
}
</style>
