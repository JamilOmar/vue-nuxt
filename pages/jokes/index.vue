<template>
  <div>
    <SearchJokes v-on:search-text="searchText" />
    <Joke v-for="joke in jokes" :key="joke.id" :id="joke.id" :joke="joke.joke" />
  </div>
</template>

<script>
import axios from "axios";
import SearchJokes from "../../components/SearchJokes";
import Joke from "../../components/Joke";
export default {
  components: {
    SearchJokes,
    Joke
  },
  data() {
    return {
      jokes: []
    };
  },
  methods: {
    async searchText(text) {
      const config = {
        headers: {
          Accept: "application/json"
        }
      };
      try {
        const resp = await axios.get(
          `https://icanhazdadjoke.com/search?term=${text}`,
          config
        );
        this.jokes = resp.data.results;
      } catch (err) {
        console.log(err);
      }
    }
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const resp = await axios.get("https://icanhazdadjoke.com/search", config);
      this.jokes = resp.data.results;
    } catch (err) {
      console.log(err);
    }
  },
  head() {
    return {
      title: "Dad Jokes",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Best place for corny dad jokes"
        }
      ]
    };
  }
};
</script>

<style>
</style>