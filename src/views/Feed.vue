<template>
  <v-container>
    <div v-for="meme in memes" :key="meme.id">
      <div class="memeContainer">
        <router-link :to="`/meme/${meme.id}`">
          <meme
            class="memeImage"
            :top="meme.topText"
            :bottom="meme.bottomText"
            :imageURL="meme.imageURL"
          />
        </router-link>
      </div>
    </div>
    <div class="footer"></div>
  </v-container>
</template>

<script>
import { db } from "../firebase";
import Meme from "../components/Meme";

export default {
  components: { Meme },
  data() {
    return {
      memes: [],
    };
  },

  mounted() {
    db.collection("memes").onSnapshot((snap) => {
      const memes = snap.docs.map((doc) => {
        return {
          ...doc.data(),
          id: doc.id,
        };
      });
      this.memes = memes;
    });
  },
};
</script>

<style scoped>
.footer {
  height: 5em;
}

.memeContainer {
  display: flex;
  justify-content: center;
  margin-top: 5em;
  margin-bottom: -3em;
}

.memeImage {
  border: 4px;
  border-color: black;
  border-style: solid;
}
</style>