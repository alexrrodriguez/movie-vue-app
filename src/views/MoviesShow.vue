<template>
  <div class="movies-show">
    <div class="row">
      <div class="col-sm-12">
        <div class="card">
          <div class="card-body">
            <h2 class="card-title">{{ movie.title }} - {{ movie.year }}</h2>
            <h5>{{ movie.director }}</h5>
            <p class="card-text">{{ movie.plot }}</p>
            <router-link v-bind:to="`/movies/${movie.id}/edit`">Edit Movie</router-link>
            |
            <button v-on:click="destroyMovie(movie)">Delete Movie</button>
            |
            <router-link to="/movies">Back to all Movies</router-link>
          </div>
        </div>
      </div>
    </div>
    <!-- <h2 style="background-color: Violet">{{ movie.title }}</h2>
    <p style="border: 2px solid Violet">{{ movie.director }}</p>
    <p style="color: Tomato">{{ movie.year }}</p>
    <p>{{ movie.plot }}</p>
    <router-link v-bind:to="`/movies/${movie.id}/edit`">Edit Movie</router-link>
    |
    <button v-on:click="destroyMovie(movie)">Delete Movie</button>
    |
    <router-link to="/movies">Back to all Movies</router-link> -->
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios.get("/movies/" + this.$route.params.id).then((response) => {
      console.log("movies show", response);
      this.movie = response.data;
    });
  },
  methods: {
    destroyMovie: function (movie) {
      axios.delete("/movies/" + movie.id).then((response) => {
        console.log("movies destroy", response);
        this.$router.push("/movies");
      });
    },
  },
};
</script>
