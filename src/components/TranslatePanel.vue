<template>
  <div class="page">
    <TranslateInput :text="message" :handleChangeText="handleChangeText" />

    <img
      alt="Icon pointing result"
      class="arrow"
      src="../assets/arrow-down-lorraine.png"
    />
    <TranslateResult :text="message" />
  </div>
</template>

<script>
import TranslateInput from "./Input.vue";
import TranslateResult from "./Result.vue";

export default {
  name: "TranslatePanel",
  components: {
    TranslateInput,
    TranslateResult,
  },
  data: function () {
    return {
      message: "",
    };
  },
  methods: {
    handleChangeText: function (message) {
      this.message = message;
    },
  },
};
</script>

<style scoped>
.page {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 80%;
  max-width: 700px;
  margin: auto;
}

.arrow {
  width: 50px;
  margin: auto;
}
</style>
