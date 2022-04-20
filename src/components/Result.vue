<template>
  <div class="container">
    <span>{{ translatedText }}</span>
  </div>
</template>

<script>
import { translate } from "lorrainjs";

export default {
  name: "TranslateResult",
  props: {
    text: String,
  },
  watch: {
    text: function (val) {
      this.translatedText = translate(val);
    },
  },
  data: function () {
    return {
      translatedText: translate(this.text),
    };
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  width: 100%;
  padding: 10px;
}
span {
  border-radius: 10px;
  width: 100%;
  background: rgba(255, 255, 255, 0.4);
  padding: 10px;
  text-align: left;
  white-space: pre;
  color: black;
  min-height: 80px;
  box-shadow: 5px 5px 5px grey;
}
</style>
