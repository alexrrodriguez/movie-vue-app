<template>
  <div class="movies-new">
    <h1 style="color: Tomato">New Movie</h1>
    <form v-on:submit.prevent="createMovie()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div class="input-group mb-3">
        <span class="input-group-text" id="inputGroup-sizing-default">Title:</span>
        <input
          type="text"
          v-model="newMovieParams.title"
          class="form-control"
          aria-label="Sizing example input"
          aria-describedby="inputGroup-sizing-default"
        />
      </div>
      <div class="input-group mb-3">
        <span class="input-group-text" id="inputGroup-sizing-default">Plot:</span>
        <textarea
          type="text"
          v-model="newMovieParams.plot"
          class="form-control"
          aria-label="Sizing example input"
          aria-describedby="inputGroup-sizing-default"
          name=""
          id=""
          cols="20"
          rows="5"
        ></textarea>

        <!-- <input
          type="text"
          v-model="newMovieParams.director"
          class="form-control"
          aria-label="Sizing example input"
          aria-describedby="inputGroup-sizing-default"
        /> -->
      </div>
      <small v-if="newMovieParams.plot.length > 400" class="text-danger">Characters must not exceed 400</small>
      <div class="input-group mb-3">
        <span class="input-group-text" id="inputGroup-sizing-default">Year:</span>
        <input
          type="text"
          v-model="newMovieParams.year"
          class="form-control"
          aria-label="Sizing example input"
          aria-describedby="inputGroup-sizing-default"
        />
      </div>
      <div class="input-group mb-3">
        <span class="input-group-text" id="inputGroup-sizing-default">Director:</span>
        <input
          type="text"
          v-model="newMovieParams.director"
          class="form-control"
          aria-label="Sizing example input"
          aria-describedby="inputGroup-sizing-default"
        />
      </div>
      <!-- Title:
      <input type="text" v-model="newMovieParams.title" />
      Director:
      <input type="text" v-model="newMovieParams.director" />
      Year:
      <input type="text" v-model="newMovieParams.year" />
      Plot:
      <input type="text" v-model="newMovieParams.plot" /> -->
      <input class="btn btn-primary" type="submit" value="Create" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newMovieParams: { plot: "" },
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createMovie: function () {
      axios
        .post("/movies", this.newMovieParams)
        .then((response) => {
          console.log("movies create", response);
          this.$router.push("/movies");
        })
        .catch((error) => {
          console.log("movies create error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
