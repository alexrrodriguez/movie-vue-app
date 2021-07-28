<template>
  <div class="actor-new">
    <h1 style="color: Tomato">New Actor</h1>
    <form v-on:submit.prevent="createActor()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div class="input-group mb-3">
        <span class="input-group-text" id="inputGroup-sizing-default">First Name</span>
        <input
          type="text"
          v-model="newActorParams.first_name"
          class="form-control"
          aria-label="Sizing example input"
          aria-describedby="inputGroup-sizing-default"
        />
      </div>
      <div class="input-group mb-3">
        <span class="input-group-text" id="inputGroup-sizing-default">Last Name</span>
        <input
          type="text"
          v-model="newActorParams.last_name"
          class="form-control"
          aria-label="Sizing example input"
          aria-describedby="inputGroup-sizing-default"
        />
      </div>
      <div class="input-group mb-3">
        <span class="input-group-text" id="inputGroup-sizing-default">Known For</span>
        <input
          type="text"
          v-model="newActorParams.known_for"
          class="form-control"
          aria-label="Sizing example input"
          aria-describedby="inputGroup-sizing-default"
        />
      </div>
      <div class="input-group mb-3">
        <span class="input-group-text" id="inputGroup-sizing-default">Gender</span>
        <input
          type="text"
          v-model="newActorParams.gender"
          class="form-control"
          aria-label="Sizing example input"
          aria-describedby="inputGroup-sizing-default"
        />
      </div>
      <div class="input-group mb-3">
        <span class="input-group-text" id="inputGroup-sizing-default">Age</span>
        <input
          type="text"
          v-model="newActorParams.age"
          class="form-control"
          aria-label="Sizing example input"
          aria-describedby="inputGroup-sizing-default"
        />
      </div>
      <div class="input-group mb-3">
        <span class="input-group-text" id="inputGroup-sizing-default">Image</span>
        <input
          type="text"
          v-model="newActorParams.image"
          class="form-control"
          aria-label="Sizing example input"
          aria-describedby="inputGroup-sizing-default"
        />
      </div>
      <div class="input-group mb-3">
        <span class="input-group-text" id="inputGroup-sizing-default">Movie ID</span>
        <input
          type="text"
          v-model="newActorParams.movie_id"
          class="form-control"
          aria-label="Sizing example input"
          aria-describedby="inputGroup-sizing-default"
        />
      </div>
      <!-- First Name:
      <input type="text" v-model="newActorParams.first_name" /> -->
      <!-- Last Name:
      <input type="text" v-model="newActorParams.last_name" />
      Known For:
      <input type="text" v-model="newActorParams.known_for" />
      Gender:
      <input type="text" v-model="newActorParams.gender" />
      Age:
      <input type="text" v-model="newActorParams.age" />
      Image:
      <input type="text" v-model="newActorParams.image" />
      Movie-ID:
      <input type="text" v-model="newActorParams.movie_id" /> -->
      <input class="btn btn-primary" type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newActorParams: {},
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createActor: function () {
      axios
        .post("/actors", this.newActorParams)
        .then((response) => {
          console.log("actors create", response);
          this.$router.push("/actors");
        })
        .catch((error) => {
          console.log("actors create error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
