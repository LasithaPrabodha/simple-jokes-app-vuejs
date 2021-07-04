<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <Jokes title="Jokes" />
  </div>
</template>

<script>
// @ is an alias to /src
import Jokes from "@/components/Jokes.vue";

export default {
  name: "Home",
  components: {
    Jokes,
  },
};
</script>
