<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>

  <p>
    Ask a yes/no question:
    <input v-model="question" />
  </p>

  <p>{{ answer }}</p>

  <div>
    <img v-bind:src="img" />
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "About",
  data() {
    return {
      question: "",
      answer: "",
      img: "",
    };
  },
  watch: {
    question(newQuestion) {
      if (newQuestion.indexOf("?") > 0) {
        this.getAnswer();
      }
    },
  },
  methods: {
    getAnswer() {
      this.answer = "Thinking...";

      axios
        .get("https://yesno.wtf/api")
        .then((reponse) => {
          this.answer = reponse.data.answer;
          this.img = reponse.data.image;
        })
        .catch((error) => {
          this.answer = "";
          alert("Error! Could not reach the API. " + error);
        });
    },
  },
};
</script>

<style scoped>
img {
  width: 30em;
}
</style>