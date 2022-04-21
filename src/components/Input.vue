<template>
  <div class="container">
    <textarea
      v-model="message"
      placeholder="Ecrit le texte à traduire ici"
      rows="4"
      autofocus
    ></textarea>
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
  align-items: center;
  width: 100%;
  padding: 10px;
}
textarea {
  display: flex;
  border-radius: 10px;
  width: 100%;
  background: rgba(255, 255, 255, 0.4);
  padding: 10px;
  resize: none;
  font-size: large;
  box-shadow: 5px 5px 5px grey;
}

textarea:focus {
  outline-offset: unset !important;
  outline: unset !important;
}

textarea:focus-visible {
  outline-offset: unset !important;
  outline: unset !important;
}
</style>
