<template>
  <Quote v-bind:text="quote" v-bind:author="author" v-bind:fetching="fetching" v-bind:next="fetchData" />
</template>

<script lang="ts">
import Vue from "vue";
import Quote from "./components/Quote.vue";

export default Vue.extend({
  name: "app",
  components: {
    Quote
  },
  data: function() {
    return {
      author: "",
      quote: "",
      fetching: false
    };
  },
  created: function() {
    this.fetchData();
  },
  methods: {
    fetchData: function() {
      const url = "https://thesimpsonsquoteapi.glitch.me/quotes";
      this.fetching = true;
      fetch(url)
        .then(res => res.json())
        .then(data => {
          console.log(data);
          this.author = data[0].character;
          this.quote = data[0].quote;
          this.fetching = false;
        });
    }
  }
});
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Open+Sans:400,600");

body {
  margin: 0;
  padding: 0;
  --color-white: rgba(255, 255, 255, 0.87);
  --accent-color: #d6c6b2;
  background-color: #21272b;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: var(--color-white);
  font-family: "Open Sans", sans-serif;
}
</style>
