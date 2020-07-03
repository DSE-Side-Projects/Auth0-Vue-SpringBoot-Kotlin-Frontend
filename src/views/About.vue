<template>
  <div class="about">
    <h1>This is an about page</h1>
    <button @click="callAPI">Call API</button>
    <h2>{{ greeting }}</h2>
  </div>
</template>

<script>
import axios from "axios"; // HTTP client module
import authService from "../../auth/authService";
export default {
  name: "about",
  data() {
    return {
      greeting: "",
      accessToken: null
    };
  },
  created() {
    this.accessToken = authService.accessToken;
  },
  methods: {
    // calls the helloworld endpoint from the backend and updates the greeting data attribute which reactively updates the template with the helloworld! message
    callAPI() {
      axios({
        method: "GET",
        url: "http://localhost:8888/helloworld",
        headers: { authorization: `Bearer ${this.accessToken}` }
      })
        .then(resp => {
          this.greeting = resp.data;
        })
        .catch(err => {
          this.greeting = err;
        });
    }
  }
};
</script>
