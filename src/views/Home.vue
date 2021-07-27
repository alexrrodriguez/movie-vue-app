<template>
  <div class="home">
    <h2>Add a Movie!</h2>
    <div>
      Title:
      <input type="text" v-model="newMovieParams.title" />
      Year:
      <input type="text" v-model="newMovieParams.year" />
      Plot:
      <input type="text" v-model="newMovieParams.plot" />
      Director:
      <input type="text" v-model="newMovieParams.director" />
      <button v-on:click="createMovie()">Create Movie</button>
    </div>
    <h1>{{ message }}</h1>
    <div v-for="movie in movies" :key="movie.id">
      <h2 style="background-color: Violet">Title: {{ movie.title }}</h2>
      <h2 style="border: 2px solid Violet">Year: {{ movie.year }}</h2>
      <h2 style="color: Tomato">Director: {{ movie.director }}</h2>
      <h2>Plot: {{ movie.plot }}</h2>
      <button v-on:click="showMovie(movie)">More Info</button>
    </div>
    <dialog id="movie-details">
      <form method="dialog">
        <h1>Movie Info</h1>
        <p>
          Title:
          <input type="text" v-model="currentMovie.title" />
        </p>
        <p>
          Year:
          <input type="text" v-model="currentMovie.year" />
        </p>
        <p>
          Plot:
          <input type="text" v-model="currentMovie.plot" />
        </p>
        <p>
          Director:
          <input type="text" v-model="currentMovie.director" />
        </p>
        <button v-on:click="updateMovie(currentMovie)">Update</button>
        <button v-on:click="destroyMovie(currentMovie)">Delete</button>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>
<style></style>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Here are some movies!",
      movies: [],
      newMovieParams: {},
      currentMovie: {},
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/movies").then((response) => {
        this.movies = response.data;
        console.log("Movies:", this.movies);
      });
    },
    createMovie: function () {
      axios
        .post("/movies", this.newMovieParams)
        .then((response) => {
          console.log("Success!", response);
          this.movies.push(response.data);
          this.newMovieParams = {};
        })
        .catch((error) => {
          console.log("movie create error", error.response);
        });
    },
    showMovie: function (movie) {
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
    updateMovie: function (movie) {
      var editMovieParams = movie;
      axios
        .patch("/movies/" + movie.id, editMovieParams)
        .then((response) => {
          console.log("movies update", response);
          this.currentMovie = {};
        })
        .catch((error) => {
          console.log("movies update error", error.response);
        });
    },
    destroyMovie: function (movie) {
      axios.delete("/movies/" + movie.id).then((response) => {
        console.log("movie deleted", response);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    },
  },
};
</script>
