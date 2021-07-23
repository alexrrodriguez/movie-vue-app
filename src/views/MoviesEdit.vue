<template>
  <div class="movies-edit">
    <h1>Edit Movie</h1>
    <form v-on:submit.prevent="updateMovie(movie)">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Title:
      <input type="text" v-model="movie.title" />
      Director:
      <input type="text" v-model="movie.director" />
      Year:
      <input type="text" v-model="movie.year" />
      Plot:
      <input type="text" v-model="movie.plot" />
      <input type="submit" value="Update" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("/movies/" + this.$route.params.id).then((response) => {
      console.log("movies show", response);
      this.movie = response.data;
    });
  },
  methods: {
    updateMovie: function (movie) {
      var editMovieParams = movie;
      axios
        .patch("/movies/" + movie.id, editMovieParams)
        .then((response) => {
          console.log("movies update", response);
          this.$router.push("/movies");
        })
        .catch((error) => {
          console.log("movies update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
