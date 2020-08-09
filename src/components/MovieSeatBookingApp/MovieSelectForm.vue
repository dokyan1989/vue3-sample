<template>
  <div class="movie-container">
    <label>Pick a movie:</label>
    <select v-bind:value="modelValue" v-on:change="handleChange">
      <option
        v-for="movie in movies"
        v-bind:value="movie.price"
        v-bind:key="movie.id"
      >{{ movie.name }} (${{movie.price}})</option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'MovieSelectForm',
  props: {
    movies: Array,
    modelValue: Number,
  },
  methods: {
    handleChange(event) {
      localStorage.setItem('selectedMoviePrice', +event.target.value)
      this.$emit('update:modelValue', +event.target.value)
    },
  },
}
</script>

<style scoped>
.movie-container {
  margin: 20px 0;
}

.movie-container select {
  background-color: #fff;
  border: 0;
  border-radius: 5px;
  font-size: 14px;
  margin-left: 10px;
  padding: 5px 15px 5px 15px;
  -moz-appearance: none;
  -webkit-appearance: none;
  appearance: none;
}
</style>