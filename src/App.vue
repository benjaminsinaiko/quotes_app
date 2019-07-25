<template>
  <div id="app">
    <div class="quote-list">
      <QuoteItem v-for="quote in paginatedQuotes" :quote="quote" :key="quote.quote" />
    </div>

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
  data() {
    return {
      quotes: [],
      pageNumber: 0,
      quotesPerPage: 10,
      displayQuotes: []
    };
  },
  mounted() {
    this.getQuotes();
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
  },
  methods: {
    getQuotes() {
      const url =
        "https://gist.githubusercontent.com/benchprep/dffc3bffa9704626aa8832a3b4de5b27/raw/quotes.json";
      axios
        .get(url)
        .then(res => {
          this.quotes = res.data;
        })
        .catch(err => console.console.error(err));
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
  width: 100%;
}
.quote-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: auto;
  max-width: 1000px;
}
</style>
