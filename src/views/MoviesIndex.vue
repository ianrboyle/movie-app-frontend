<template>
  <div class="movies-index">
    <h1>{{ message }}</h1>
    Search by title:
    <input v-model="titleFilter" />
    Search by name:
    <input v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
    </datalist>
    <div>
      <button>Sort Alphabetically</button>
    </div>
    <div v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), 'title')" :key="movie.id">
      <h3>{{ movie.title }}</h3>
      <router-link v-bind:to="`/movies/${movie.id}`">Movie Info</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";
export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      message: "Welcome to the movies index page.",
      movies: [],
      titleFilter: "",
    };
  },
  created: function () {
    axios.get("http://localhost:3000/movies").then((response) => {
      this.movies = response.data;
      console.log("Movies:", response.data);
    });
  },
};
</script>
