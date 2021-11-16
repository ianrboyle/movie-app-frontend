<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <h1>{{ message }}</h1>
    <div class="movies-index">
      <p>{{ message }}</p>
      <div v-for="movie in movies" :key="movie.id">
        <p>{{ movie.title }}</p>
        <button v-on:click="showMovie(movie)">Movie Info</button>
      </div>
      <dialog id="movie-details">
        <form method="dialog">
          <div>
            <label>Title:</label>
            <input type="text" v-model="currentMovie.title" />
          </div>
          <div>
            <label>Plot:</label>
            <input type="text" v-model="currentMovie.plot" />
          </div>
          <div>
            <label>Year:</label>
            <input type="text" v-model="currentMovie.year" />
          </div>
          <button>Close</button>
          |
          <button v-on:click="updateMovie(currentMovie)">Update</button>
          |
          <button v-on:click="deleteMovie(currentMovie)">Delete</button>
        </form>
      </dialog>
    </div>
    <div class="movies-new">
      <form v-on:submit.prevent="createMovie()">
        <h1>New Movie!</h1>
        <ul>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
        <div>
          <label>Title:</label>
          <input type="text" v-model="newMovieParams.title" />
        </div>
        <div>
          <label>Year:</label>
          <input type="text" v-model="newMovieParams.year" />
        </div>
        <div>
          <label>Plot:</label>
          <input type="text" v-model="newMovieParams.plot" />
        </div>
        <div>
          <label>Director:</label>
          <input type="text" v-model="newMovieParams.director" />
        </div>
        <div>
          <label>In English?:</label>
          <input type="text" v-model="newMovieParams.english" />
        </div>
        <input type="submit" value="Submit" />
      </form>
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
      newMovieParams: {},
      errors: {},
      currentMovie: {},
    };
  },
  created: function () {
    axios.get("http://localhost:3000/movies").then((response) => {
      this.movies = response.data;
      console.log("Movies:", response.data);
    });
  },
  methods: {
    createMovie: function () {
      axios
        .post("http://localhost:3000/movies", this.newMovieParams)
        .then(() => {
          this.$router.push("/movies");
          console.log("Success!");
        })
        .catch((error) => console.log(error.response));
    },
    showMovie: function (movie) {
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
    updateMovie: function (movie) {
      axios.patch("http://localhost:3000/movies/" + movie.id, movie).then((response) => {
        console.log("Success", response.data);
      });
    },
    deleteMovie: function (movie) {
      axios.delete("http://localhost:3000/movies/" + movie.id, movie).then((response) => {
        console.log("DELETED!", response.data);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    },
  },
};
</script>
