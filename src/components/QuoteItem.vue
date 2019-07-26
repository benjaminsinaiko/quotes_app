<template>
  <div class="card" :class="{games: quote.theme === 'games', movies: quote.theme === 'movies'}">
    <h2 class="quote-context">{{quote.context}}</h2>
    <p class="quote-text">"{{quote.quote}}"</p>
    <p class="quote-source">--{{quote.source}}</p>
  </div>
</template>

<script>
export default {
  name: "QuotesItem",
  props: ["quote"]
};
</script>

<style>
.card {
  height: auto;
  width: 80%;
  padding: 20px;
  margin: 12px;
  box-shadow: 6px 6px 2px 1px rgba(0, 0, 0, 0.2);
}
.movies {
  background-color: #d9ffe4;
}
.games {
  background-color: #fffdd9;
}
.quote-context {
  text-transform: uppercase;
}
.quote-text {
  font-style: italic;
}
.quote-source {
  text-align: right;
}
</style>