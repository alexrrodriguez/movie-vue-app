<template>
  <div class="actors-show">
    <h2 class="card-title">{{ actor.first_name }} {{ actor.last_name }}</h2>
    <img v-bind:src="actor.image" v-bind:alt="actor.last_name" />
    <p>Gender: {{ actor.gender }}</p>
    <p>Age: {{ actor.age }}</p>
    <p>Known For: {{ actor.known_for }}</p>
    <router-link v-bind:to="`/actors/${actor.id}/edit`">Edit Actor</router-link>
    |
    <button v-on:click="destroyActor(actor)">Delete Actor</button>
    |
    <router-link to="/actors">Back to all Actors</router-link>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      actor: {},
    };
  },
  created: function () {
    axios.get("/actors/" + this.$route.params.id).then((response) => {
      console.log("actors show", response);
      this.actor = response.data;
    });
  },
  methods: {
    destroyActor: function (actor) {
      axios.delete("/actors/" + actor.id).then((response) => {
        console.log("actors destroy", response);
        this.$router.push("/actors");
      });
    },
  },
};
</script>
