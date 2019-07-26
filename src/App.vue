<template>
  <div id="app">
    <header>Quotes App</header>
    <div class="filters">
      <CategorySelector :quoteCategory="quoteCategory" @setCategory="setCategory" />
      <QuoteSearch />
    </div>
    <div class="quote-list">
      <QuoteItem v-for="quote in paginatedQuotes" :quote="quote" :key="quote.id" />
    </div>
    <button @click="prevPage()" class="float prev" v-show="pageNumber !== 0">Page -</button>
    <button @click="nextPage()" class="float next" v-show="pageNumber < pageCount -1">Page +</button>
  </div>
</template>

<script>
import axios from "axios";
import CategorySelector from "./components/CategorySelector.vue";
import QuoteSearch from "./components/QuoteSearch.vue";
import QuoteItem from "./components/QuoteItem.vue";

export default {
  name: "app",
  components: {
    CategorySelector,
    QuoteSearch,
    QuoteItem
  },
  data() {
    return {
      quotes: [],
      pageNumber: 0,
      quotesPerPage: 10,
      displayQuotes: [],
      quoteCategory: "all"
    };
  },
  watch: {
    // update displayQuotes and reset to page 0
    quoteCategory: function() {
      if (this.quoteCategory === "all") {
        this.displayQuotes = this.quotes;
      } else {
        this.displayQuotes = this.quotes.filter(
          quote => quote.theme === this.quoteCategory
        );
      }
      return (this.pageNumber = 0);
    }
  },
  mounted() {
    this.getQuotes();
  },
  computed: {
    // count num pages
    pageCount() {
      const numQuotes = this.displayQuotes.length;
      return Math.ceil(numQuotes / this.quotesPerPage);
    },
    // quotes to display
    paginatedQuotes() {
      const first = this.pageNumber * this.quotesPerPage;
      const last = first + this.quotesPerPage;
      return this.displayQuotes.slice(first, last);
    }
  },
  methods: {
    getQuotes() {
      const url =
        "https://gist.githubusercontent.com/benchprep/dffc3bffa9704626aa8832a3b4de5b27/raw/quotes.json";
      axios
        .get(url)
        .then(res => {
          let id = 1;
          const quoteResults = res.data;
          quoteResults.map(quote => {
            quote.id = id;
            id++;
          });
          this.quotes = quoteResults;
          this.displayQuotes = quoteResults;
        })
        .catch(err => console.console.error(err));
    },
    setCategory(category) {
      this.quoteCategory = category;
    },
    prevPage() {
      this.pageNumber--;
      window.scrollTo(0, 0);
    },
    nextPage() {
      this.pageNumber++;
      window.scrollTo(0, 0);
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
header {
  position: fixed;
  color: #fff;
  background-color: rgba(0, 88, 204, 0.534);
  top: 0;
  width: 100%;
  height: 60px;
  font-size: 2.5rem;
  font-weight: bold;
  text-align: left;
  padding-left: 20px;
  margin-left: -8px;
  margin-right: 8px;
}
.filters {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.quote-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: auto;
  max-width: 1000px;
}
.float {
  position: fixed;
  width: 60px;
  height: 60px;
  bottom: 40px;
  right: 25px;
  background-color: rgba(0, 88, 204, 0.534);
  color: #fff;
  border-radius: 50px;
  text-align: center;
  box-shadow: 2px 2px 3px #999;
}
.prev {
  left: 25px;
}
</style>
