<template>
  <h3>{{ title }}</h3>
  <p v-show="isLoading">
    <i>Thinking...</i>
  </p>

  <div v-for="joke in jokes" :key="joke.id">
    <a href="javascript:void(0)">
      <h3 @click="joke.show = !joke.show">{{ joke.setup }}</h3>
    </a>
    <p v-show="joke.show">{{ joke.punchline }}</p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Jokes",
  props: {
    title: String,
  },
  data() {
    return {
      isLoading: false,
      jokes: [],
      errorMsg: "",
    };
  },
  mounted() {
    this.loadJokes();
  },
  methods: {
    loadJokes() {
      this.isLoading = true;
      axios
        .get("https://official-joke-api.appspot.com/jokes/ten")
        .then((response) => {
          this.isLoading = false;

          this.jokes = response.data.map((joke) => ({ ...joke, show: false }));
        })
        .catch(() => {
          this.isLoading = false;

          alert("Error! No jokes. ");
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
