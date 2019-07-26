<template>
  <div class="category-select">
    <form>
      <p class="select-title">Quotes Category</p>
      <select
        v-model="category"
        @change="emitSelect"
        aria-placeholder="category"
        :class="{games: category === 'games', movies: category === 'movies'}"
      >
        <option :value="undefined">Select Category</option>
        <option v-for="category in categories" :selected="category" :key="category">{{ category }}</option>
      </select>
    </form>
  </div>
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
  watch: {
    quoteCategory() {
      this.category = this.quoteCategory;
    }
  },
  methods: {
    emitSelect(e) {
      this.$emit("setCategory", e.target.value);
    }
  }
};
</script>

<style scoped>
.category-select {
  margin-right: 50px;
}
select {
  width: 130px;
  height: 30px;
  text-align-last: center;
  text-transform: uppercase;
}
p {
  margin-bottom: 5px;
}
.movies {
  background-color: #d9ffe4;
}
.games {
  background-color: #fffdd9;
}
</style>