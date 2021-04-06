<template>
  <div>
    <div class="navbar_spacer"></div>
    <v-img :src="imageURL" :width="800">
      <h1 id="top">{{ top.toUpperCase() }}</h1>
      <h1 id="bottom">{{ bottom.toUpperCase() }}</h1>
    </v-img>
  </div>
</template>

<script>
export default {
  props: ["top", "bottom", "imageURL"],
};
</script>

<style>
.navbar_spacer {
  height: 5em;
}
</style>