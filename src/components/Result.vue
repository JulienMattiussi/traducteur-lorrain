<template>
  <div class="container">
    <div class="result">
      <span>{{ translatedText }}</span>
    </div>
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
}
.result {
  display: flex;
  align-items: center;
  gap: 10px;
}
</style>
