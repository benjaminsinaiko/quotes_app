<template>
  <div id="app">
    <QuoteItem v-for="quote in paginatedQuotes" :quote="quote" :key="quote.quote" />

    <!-- <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />-->
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import QuoteItem from "./components/QuoteItem.vue";
import axios from "axios";

export default {
  name: "app",
  components: {
    HelloWorld,
    QuoteItem
  },
  data: function() {
    return {
      quotes: [],
      pageNumber: 0,
      quotesPerPage: 10,
      displayQuotes: []
    };
  },
  mounted: function() {
    axios
      .get(
        "https://gist.githubusercontent.com/benchprep/dffc3bffa9704626aa8832a3b4de5b27/raw/quotes.json"
      )
      .then(res => {
        this.quotes = res.data;
      });
  },
  computed: {
    // count num pages
    pageCount() {
      const numQuotes = this.quotes.length;
      return Math.ceil(numQuotes / this.quotesPerPage);
    },
    // quotes to display
    paginatedQuotes() {
      const first = this.pageNumber * this.quotesPerPage;
      const last = first + this.quotesPerPage;

      return this.quotes.slice(first, last);
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
