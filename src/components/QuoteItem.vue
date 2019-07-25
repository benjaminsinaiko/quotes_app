<template>
  <div>
    <h2>{{quote.context}}</h2>
    <p>"{{quote.quote}}"</p>
    <p>--{{quote.source}}</p>
  </div>
</template>

<script>
export default {
  name: "QuotesItem",
  props: ["quote"],
  methods: {},
  compiled: function() {
    console.log("hello");
  }
};
</script>