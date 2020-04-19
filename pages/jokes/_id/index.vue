<template>
  <div>
    <nuxt-link to="/jokes">Back to Jokes</nuxt-link>
    <h2>{{joke}}</h2>
    <hr />
    <small>Joke ID:{{$route.params.id}}</small>
  </div>
</template>

<script>
import axios from "axios";
export default {
  head() {
    return {
      title:`Joke ${this.$route.params.id}`,
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Best place for corny dad jokes"
        }
      ]
    };
  },
  data() {
    return {
      joke: {}
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const resp = await axios.get(
        `https://icanhazdadjoke.com/j/${this.$route.params.id}`,
        config
      );
      this.joke = resp.data.joke;
    } catch (err) {
      console.log(err);
    }
  }
};
</script>

<style>
</style>