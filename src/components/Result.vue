<template>
  <div class="container">
    <span class="result">{{ translatedText }}</span>
    <span id="log"></span>
  </div>
</template>

<script>
import { translate, initAll } from "lorrainjs";

const limit = 300;

const scrollToBottom = (node) => {
  node.scrollTop = node.scrollHeight;
};

function debouncer(fn, delay) {
  let timeoutID = null;
  let argsRef = "";
  return function () {
    const args = arguments;
    const currentArgs = Array.from(args).reduce(
      (arg, fullString) => `${fullString}+${arg.toString()}`,
      ""
    );
    if (argsRef === currentArgs) {
      clearTimeout(timeoutID);
    } else {
      argsRef = `${currentArgs}`;
    }
    const that = this;
    timeoutID = setTimeout(function () {
      fn.apply(that, args);
    }, delay);
  };
}

function convertStringToJSON(source) {
  return source.replace(/(\w+:)|(\w+ :)/g, function (matchedStr) {
    return '"' + matchedStr.substring(0, matchedStr.length - 1) + '":';
  });
}

export default {
  name: "TranslateResult",
  props: {
    text: String,
  },
  mounted() {
    (function () {
      initAll();
      const logger = document.getElementById("log");
      const oldLog = console.log;
      const oldWarn = console.warn;
      const oldError = console.error;

      const logInScreen = debouncer((message, level) => {
        let color = "inherit";
        let icon = "&nbsp;";

        switch (level) {
          case "warn": {
            color = "#8B4513";
            icon = "⚠️";
            break;
          }
          case "error": {
            color = "#800000";
            icon = "⛔";
          }
        }
        logger.innerHTML = `${
          logger.innerHTML
        }<p style="margin: 0;color:${color};display:flex;"><span style="width: 25px;font-size: 15px;">${icon}</span> ${translate(
          message
        )}</p>`;
        scrollToBottom(logger);
      }, 300);

      console.log = function (message) {
        oldLog(message);
        logInScreen(message, "log");
      };

      console.warn = function (message) {
        oldWarn(message);
        logInScreen(message, "warn");
      };

      console.error = function (message) {
        oldError(message);
        logInScreen(message, "error");
      };
    })();
  },
  watch: {
    text: function (val) {
      if (!val) {
        console.warn("Le texte à été effacé.");
        return;
      }
      if (val.length > limit) {
        console.error(new Error(`Limite de ${limit} caractères atteinte.`));
        return;
      }
      try {
        const jsonString = convertStringToJSON(val);
        const jsonObject = JSON.parse(jsonString);
        if (this.sourceType !== "object") {
          console.log("La source est un objet valide.");
        }

        const newTranslation = translate(jsonObject);
        if (this.translatedText !== newTranslation) {
          console.log("L'objet à été modifié.");
          this.translatedText = newTranslation;
        }
        this.sourceType = "object";
      } catch (error) {
        if (this.sourceType !== "text") {
          console.log("La source est un texte.");
        }
        const newTranslation = translate(val);
        if (this.translatedText !== newTranslation) {
          this.translatedText = translate(val);
          console.log("Le texte à été modifié.");
        }
        this.sourceType = "text";
      }
    },
  },
  data: function () {
    return {
      translatedText: translate(this.text),
      sourceType: "text",
    };
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
span.result {
  display: flex;
  border-radius: 10px;
  width: 100%;
  background: rgba(255, 255, 255, 0.4);
  padding: 10px;
  text-align: left;
  white-space: pre;
  color: black;
  min-height: 80px;
  max-height: 200px;
  overflow-y: auto;
  box-shadow: 5px 5px 5px grey;
}

span#log {
  display: flex;
  flex-direction: column;
  margin-top: 10px;
  text-align: left;
  height: 80px;
  width: 400px;
  max-height: 80px;
  overflow-y: auto;
}
</style>
