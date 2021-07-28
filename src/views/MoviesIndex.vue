<template>
  <div class="movies-index">
    <h1 style="color: Tomato">All Movies</h1>
    <div class="row" v-for="movie in movies" v-bind:key="movie.id">
      <div class="col-sm-2"></div>
      <div class="col-sm-8">
        <div class="card">
          <div class="card-body">
            <h2 class="card-title">{{ movie.title }} - {{ movie.year }}</h2>
            <h5>{{ movie.director }}</h5>
            <p class="card-text">{{ movie.plot }}</p>
            <router-link class="btn btn-primary" v-bind:to="`/movies/${movie.id}`">More Info</router-link>
          </div>
        </div>
      </div>
      <!-- <div class="col-sm-4"></div> -->
    </div>
    <!-- <div v-for="movie in movies" v-bind:key="movie.id">
      <h2 style="background-color: Violet">{{ movie.title }}</h2>
      <p style="border: 2px solid Violet">{{ movie.director }}</p>
      <p style="color: Tomato">{{ movie.year }}</p>
      <p>{{ movie.plot }}</p>
      <router-link v-bind:to="`/movies/${movie.id}`">More Info</router-link>
    </div> -->
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/movies").then((response) => {
        console.log("movies index", response);
        this.movies = response.data;
      });
    },
  },
};
</script>
