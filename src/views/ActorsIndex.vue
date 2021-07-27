<template>
  <div class="actos-index">
    <h1>All Actors</h1>
    <div v-for="actor in actors" v-bind:key="actor.id">
      <h2>{{ actor.first_name }} {{ actor.last_name }}</h2>
      <img v-bind:src="actor.image" v-bind:alt="actor.last_name" />
      <p>Gender: {{ actor.gender }}</p>
      <p>Age: {{ actor.age }}</p>
      <p>Known For: {{ actor.known_for }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      actors: [],
    };
  },
  created: function () {
    this.indexActors();
  },
  methods: {
    indexActors: function () {
      axios.get("/actors").then((response) => {
        console.log("actors index", response);
        this.actors = response.data;
      });
    },
  },
};
</script>
