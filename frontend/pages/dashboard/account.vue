<template>
  <v-card width="600px" class="mx-auto mt-5">
    <v-card-title>
      <h1 class="display-1">Account</h1>
    </v-card-title>

    <v-card-actions>
      <v-btn class="info" v-on:click="logout()">Logout</v-btn>
    </v-card-actions>
  </v-card>
</template>




<script>
import axios from "axios";
export default {
  middleware: "isAuthenticated",
  methods: {
    logout() {
      this.$axios
        .$post("/api/v1/token/logout/")
        .then((response) => {
          axios.defaults.headers.common["Authorization"] = "";
          localStorage.removeItem("token");
          this.$store.commit("removeToken");
          this.$router.push("/");
        })
        .catch((error) => {
          if (error.response) {
            console.log(JSON.stringify(error.response.data));
          } else if (error.message) {
            console.log(JSON.stringify(error.message));
          } else {
            console.log(JSON.stringify(error));
          }
        });
    },
  },
};
</script>