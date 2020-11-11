<template>
  <v-app>
    <!-- <v-img :src="main.url" min-height="100%"> -->
      <v-card width="400px" class="mx-auto my-5">
        <v-card-title class="pb-0">
          <h1 class="mx-auto mb-5">Otto-Klaus</h1>
        </v-card-title>
        <v-card-text>
          <v-form>
            <v-text-field
              label="Usuario"
              prepend-icon="mdi-account-circle"
              v-model="user"
            />
            <v-text-field
              label="Contraseña"
              :type="showPassword ? 'text' : 'password'"
              prepend-icon="mdi-lock"
              :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
              @click:append="showPassword = !showPassword"
              v-model="password"
            />
          </v-form>
        </v-card-text>
        <v-divider></v-divider>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="info" @click="login">Login</v-btn>
        </v-card-actions>
      </v-card>
    <!-- </v-img> -->
  </v-app>
</template>

<script>
import firebase from "firebase";
import { mapState, mapActions } from "vuex";
export default {
  name: "App",
  methods: {
    ...mapActions(["updateCurrentUser"]),
    logout() {
      firebase
        .auth()
        .signOut()
        .then(() => {
          this.updateCurrentUser(null);
          this.$router.push("/login");
        });
    },
  },
  computed: {
    ...mapState(["currentUser"]),
  },
  created() {
    this.updateCurrentUser(firebase.auth().currentUser);
  },
};
</script>

<style>
</style>