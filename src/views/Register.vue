<template>
  <v-card width="400" class="mx-auto mt-5">
    <v-card-title>
      <h1 class="display-1">Login</h1>
    </v-card-title>
    <v-card-text>
      <v-form @submit.prevent="">
        <v-text-field
          label="Username"
          v-model="username"
          prepend-icon="mdi-account-circle"
        />
        <v-text-field
          :type="showPassword ? 'text' : 'password'"
          label="Password"
          v-model="password"
          prepend-icon="mdi-lock"
          :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
          @click:append="showPassword = !showPassword"
        />
      </v-form>
    </v-card-text>
    <v-card-actions>
      <v-btn type="submit" color="success" @click="register">Register</v-btn>
      <v-spacer></v-spacer>
<!--      <v-btn type="submit" color="info" @click="login">Login</v-btn>-->
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      showPassword: false,
      username: "",
      password: "",
      error: null
    };
  },
  methods: {
    register() {
      this.$store
        .dispatch("register", {
          username: this.username,
          password: this.password
        })
        .then(() => {
          this.$router.push({ name: "dashboard" });
        })
        .catch(err => {
          console.log(err.response.data);
          console.log(err.response.data.error);
          this.error = err.response.data.error;
        });
    }
  }
};
</script>

<style scoped></style>
