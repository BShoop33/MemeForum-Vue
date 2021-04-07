<template>
  <v-container>
    <form @submit.prevent="addSearch" class="searchInputContainer">
      <input
        type="text"
        class="searchInput"
        v-model="inputVal"
        placeholder=" Search for a meme"
      />
    </form>
    <div v-for="meme in displayedMemes" :key="meme.id">
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
      inputVal: "",
      searchTerm: "",
    };
  },

  mounted() {
    this.inputVal = this.$route.query.q;
    this.searchTerm = this.$route.query.q;

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

  methods: {
    addSearch() {
      this.searchTerm = this.inputVal;
      this.$router.push({
        path: "/feed",
        query: { q: this.searchTerm },
      });
    },
  },

  computed: {
    displayedMemes() {
      if (!this.searchTerm) return this.memes;

      const normalizedSearchTerm = this.searchTerm.toUpperCase();
      return this.memes.filter((m) => {
        return m.normalized.includes(normalizedSearchTerm);
      });
    },
  },
};
</script>

<style scoped>
.memeContainer {
  display: flex;
  justify-content: center;
  margin-top: -1.75em;
  margin-bottom: 3em;
}

.memeImage {
  border: 4px;
  border-color: black;
  border-style: solid;
}

.searchInputContainer {
  margin-left: 4em;
  margin-top: 5em;
  width: 15em;
}

.searchInput {
  width: 15.01em;
  border: 2px;
  border-color: black;
  border-style: solid;
}
</style>