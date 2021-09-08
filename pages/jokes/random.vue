<template>
  <div>
    <nuxt-link to="/jokes">Back To Jokes</nuxt-link>&nbsp;&nbsp;
    <router-link :to='`/jokes/random`' @click.native="$router.go()" class="sub-link">Next Random Joke</router-link>
    <h2>{{ joke }}</h2>
    <hr>
    <small>Joke ID: {{ id }}</small>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      joke: {},
      id: {}
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get( 'https://icanhazdadjoke.com/',
        config
      );
      this.joke = res.data.joke;
      this.id = res.data.id
    } catch (err) {
      console.log(err);
    }
  },
  head() {
    return {
      title: this.joke,
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