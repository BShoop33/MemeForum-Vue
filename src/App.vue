<template>
  <v-app>
    <router-view />
    <v-app-bar app color="teal darken-2" dark>
      <h1 class="header" @click="navigateHome">Vue Meme Forum</h1>
      <v-spacer></v-spacer>
      <router-link to="/create">
        <v-btn text> Create </v-btn>
      </router-link>

      <router-link to="/feed">
        <v-btn text> Memes </v-btn>
      </router-link>
    </v-app-bar>
  </v-app>
</template>

<script>
export default {
  methods: {
    navigateHome() {
      this.$router.push("/");
    },
  },
};
</script>

<style scoped>
.header {
  cursor: pointer;
}

a {
  text-decoration: none;
}
.router-link-active {
  color: rgb(255, 200, 100);
}

.router-link-active .v-btn {
  color: rgb(255, 200, 100);
}
</style>