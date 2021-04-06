<template>
  <v-app>
    <v-app-bar app color="teal darken-2" dark>
      <h1>Vue Meme Forum</h1>
      <v-spacer></v-spacer>
      <router-link to="/create"> Create </router-link>
      |
      <router-link to="/feed"> Memes </router-link>
    </v-app-bar>
  </v-app>
</template>

<script>
export default {};
</script>
