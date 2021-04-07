<template>
  <div v-if="meme">
    <meme
      class="mx-auto"
      :top="meme.topText"
      :bottom="meme.bottomText"
      :imageURL="meme.imageURL"
    />
  </div>
</template>

<script>
import { db } from "../firebase";
import Meme from "../components/Meme.vue";

export default {
  components: { Meme },
  data() {
    return {
      meme: null,
    };
  },

  async mounted() {
    const memeId = this.$route.params.memeId;
    const snapshot = await db.collection("memes").doc(memeId).get();
    this.meme = snapshot.data();
  },
};
</script>

<style>
.navbar_spacer {
  height: 5em;
}
</style>