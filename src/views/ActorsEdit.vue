<template>
  <div class="actors-edit">
    <h1>Edit Actor</h1>
    <form v-on:submit.prevent="updateActor(actor)">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      First Name:
      <input type="text" v-model="actor.first_name" />
      Last Name:
      <input type="text" v-model="actor.last_name" />
      Known For:
      <input type="text" v-model="actor.known_for" />
      Gender:
      <input type="text" v-model="actor.gender" />
      Age:
      <input type="text" v-model="actor.age" />
      Movie ID:
      <input type="text" v-model="actor.movie_id" />
      Image:
      <input type="text" v-model="actor.image" />
      |
      <input class="btn btn-primary" type="submit" value="Update" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      actor: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("/actors/" + this.$route.params.id).then((response) => {
      console.log("actors show", response);
      this.actor = response.data;
    });
  },
  methods: {
    updateActor: function (actor) {
      var editActorParams = actor;
      axios
        .patch("/actors/" + actor.id, editActorParams)
        .then((response) => {
          console.log("actors update", response);
          this.$router.push("/actors");
        })
        .catch((error) => {
          console.log("actors update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
