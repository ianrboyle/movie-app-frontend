<template>
  <div class="movies-index">
    <h1>{{ message }}</h1>
    <form v-on:submit.prevent="createMovie()">
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
        <small v-if="newMovieParams.plot.length > 0">
          {{ 200 - newMovieParams.plot.length }} characters remaining.
        </small>
        <small v-if="newMovieParams.plot.length > 200">Plot not to exceed 200 characters.</small>
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
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to the movies index page.",
      newMovieParams: { plot: "" },
    };
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
  },
};
</script>
