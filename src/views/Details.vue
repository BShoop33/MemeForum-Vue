<template>
  <div>
    <div v-if="meme" class="memeImageContainer">
      <meme
        class="memeImage"
        :top="meme.topText"
        :bottom="meme.bottomText"
        :imageURL="meme.imageURL"
      />
    </div>
    <div class="footer"></div>
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

<style scoped>
.footer {
  height: 2em;
}

.memeImage {
  border: 4px;
  border-color: black;
  border-style: solid;
}

.memeImageContainer {
  display: flex;
  justify-content: center;
  margin-top: 5.75em;
}
</style>