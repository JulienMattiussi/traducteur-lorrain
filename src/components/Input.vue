<template>
  <div class="container">
    <div class="input">
      <textarea
        v-model="message"
        placeholder="Ecrit le texte à traduire ici"
        rows="4"
      ></textarea>
    </div>
  </div>
</template>

<script>
export default {
  name: "TranslateInput",
  props: {
    text: String,
    handleChangeText: Function,
  },
  data: function () {
    return {
      message: this.text,
    };
  },
  watch: {
    message: function (val) {
      this.handleChangeText(val);
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
}
.input {
  display: flex;
  align-items: center;
  gap: 10px;
}
</style>
