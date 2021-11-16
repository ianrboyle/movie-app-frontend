<template>
  <div class="movies-index">
    <p>{{ message }}</p>
    <div v-for="movie in movies" :key="movie.id">
      <p>{{ movie.title }}</p>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to my movie app.",
      movies: [],
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
