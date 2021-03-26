<template>
  <v-app>
    <header>
      <v-app-bar color="primary" dark app>
        <v-toolbar-title style="cursor: pointer" @click="$router.push('/')"
          >Sample
        </v-toolbar-title>

        <v-spacer></v-spacer>
        <v-toolbar-items>
          <template v-if="$store.state.isAuthenticated">
            <v-btn text to="/dashboard">Dashboard</v-btn>
            <v-btn text to="/dashboard/account">Account</v-btn>
          </template>

          <template v-else>
            <v-btn text to="/">home</v-btn>
            <v-btn text to="signup">Sign up</v-btn>
            <v-btn text to="login">Login</v-btn>
          </template>
        </v-toolbar-items>
      </v-app-bar>
    </header>

    <v-main>
      <v-container>
        <!--本文内容-->
        <Nuxt />
      </v-container>
    </v-main>

    <v-footer color="primary" dark app> Copyright (c) 2021 </v-footer>
  </v-app>
</template>

<script>
import axios from "axios";
export default {
  beforeCreate() {
    this.$store.commit("initializeStore");
    const token = this.$store.state.token;
    if (token) {
      axios.defaults.headers.common["Authorization"] = "Token " + token;
    } else {
      axios.defaults.headers.common["Authorization"] = "";
    }
  },
};
</script>

<style>
</style>