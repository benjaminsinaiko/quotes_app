<template>
  <section class="category-select">
    <h5 class="select-title">Quotes Category</h5>
    <form>
      <select v-model="category" @change="emitSelect">
        <option v-for="category in categories" :selected="category" :key="category">{{ category }}</option>
      </select>
    </form>
  </section>
</template>

<script>
export default {
  name: "CategorySelector",
  props: ["quoteCategory", "setCategory"],
  data() {
    return {
      categories: ["all", "movies", "games"],
      category: this.quoteCategory
    };
  },
  methods: {
    emitSelect(e) {
      this.$emit("setCategory", e.target.value);
    }
  }
};
</script>

<style scoped>
.category-select select {
  width: 100px;
  height: 30px;
  text-align-last: center;
  text-transform: uppercase;
}
h5 {
  margin-top: 70px;
  margin-bottom: 5px;
}
</style>