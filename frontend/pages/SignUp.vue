<template>
  <v-card width="600px" class="mx-auto mt-5">
    <v-card-title>
      <h1 class="display-1">Sign up</h1>
    </v-card-title>
    <v-card-text>
      <v-form>
        <v-text-field
          v-model="username"
          prepend-icon="mdi-account-circle"
          label="E-mail"
        />
        <v-text-field
          v-model="password"
          type="password"
          prepend-icon="mdi-lock"
          label="Password"
        />

        <div class="notification is-danger" v-if="errors.length">
          <p v-for="error in errors" v-bind:key="error">
            {{ error }}
          </p>
        </div>

        <v-card-actions>
          <v-btn class="info" v-on:click="submitForm()">Sign up</v-btn>
        </v-card-actions>
      </v-form>
    </v-card-text>
  </v-card>
</template>


<script>
import axios from "axios";
export default {
  name: "SignUp",
  data() {
    return {
      username: "",
      password: "",
      errors: [],
    };
  },
  methods: {
    submitForm(e) {
      const formData = {
        username: this.username,
        password: this.password,
      };
      this.$axios
        .$post("/api/v1/users/", formData)
        .then((response) => {
          console.log(response);
          this.$router.push("/login");
        })
        .catch((error) => {
          if (error.response) {
            for (const property in error.response.data) {
              this.errors.push(`${property}: ${error.response.data[property]}`);
            }
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