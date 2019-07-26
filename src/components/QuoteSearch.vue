<template>
  <div class="search">
    <p>Search Quotes</p>
    <input v-model="query" />
    <input id="reset" type="reset" value="Reset" @click="clearForm" />
  </div>
</template>

<script>
export default {
  name: "QuerySearch",
  props: ["quoteQuery", "setQuery"],
  data() {
    return {
      query: this.quoteQuery
    };
  },
  watch: {
    query() {
      this.$emit("setQuery", this.query);
    },
    quoteQuery() {
      this.query = this.quoteQuery;
    }
  },
  methods: {
    clearForm() {
      this.query = "";
    }
  }
};
</script>

<style scoped>
.search {
  margin-left: 30px;
}
p {
  margin-bottom: 5px;
}
input {
  width: 130px;
  height: 24px;
}
input[type="reset"] {
  width: 50px;
  height: 25px;
  margin-left: 2px;
  color: #fff;
  background-color: rgba(255, 35, 35, 0.774);
}
</style>