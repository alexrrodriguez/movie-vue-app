<template>
  <div class="actos-index">
    <br />
    <div v-if="loading">
      <atom-spinner :animation-duration="1000" :size="60" :color="'#ff1d5e'" />
    </div>
    <h1 style="color: Tomato">All Actors</h1>

    <!-- <pulse-loader :loading="loading" :color="color" :size="size"></pulse-loader> -->
    <hr />
    <div class="row" v-for="actor in actors" v-bind:key="actor.id">
      <div class="col-sm-4"></div>
      <div class="col-sm-4">
        <div class="card">
          <div class="card-body">
            <h2 class="card-title">{{ actor.first_name }} {{ actor.last_name }}</h2>
            <img v-bind:src="actor.image" v-bind:alt="actor.last_name" />
            <!-- <p>Gender: {{ actor.gender }}</p>
            <p>Age: {{ actor.age }}</p> -->
            <!-- <p>Known For: {{ actor.known_for }}</p> -->
            <hr />
            <router-link class="btn btn-primary" v-bind:to="`/actors/${actor.id}`">More details</router-link>
          </div>
        </div>
      </div>
      <div class="col-sm-4"></div>
    </div>
    <!-- <div v-for="actor in actors" v-bind:key="actor.id">
      <h2>{{ actor.first_name }} {{ actor.last_name }}</h2>
      <img v-bind:src="actor.image" v-bind:alt="actor.last_name" />
      <p>Gender: {{ actor.gender }}</p>
      <p>Age: {{ actor.age }}</p>
      <p>Known For: {{ actor.known_for }}</p>
    </div> -->
  </div>
</template>
<style scoped>
img {
  max-height: 300px;
  max-width: 300px;
}
</style>
<script>
import axios from "axios";
import { AtomSpinner } from "epic-spinners";

export default {
  components: {
    AtomSpinner,
  },
  data: function () {
    return {
      actors: [],
      loading: false,
    };
  },
  created: function () {
    this.indexActors();
  },
  methods: {
    indexActors: function () {
      this.loading = true;
      axios
        .get("/actors")
        .then((response) => {
          console.log("actors index", response);
          this.actors = response.data;
        })
        .finally(() => (this.loading = false));
    },
  },
};
</script>
