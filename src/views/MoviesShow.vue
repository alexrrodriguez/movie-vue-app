<template>
  <div class="movies-show">
    <h2>{{ movie.title }}</h2>
    <p>{{ movie.director }}</p>
    <p>{{ movie.year }}</p>
    <p>{{ movie.plot }}</p>
    <router-link v-bind:to="`/movies/${movie.id}/edit`">Edit Movie</router-link>
    |
    <router-link to="/movies">Back to all Movies</router-link>
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
  methods: {},
};
</script>
