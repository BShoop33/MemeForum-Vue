<template>
  <v-container>
    <v-form class="memeForm" @submit.prevent="generateMeme">
      <v-row justify="space-between">
        <v-col>
          <v-text-field
            outlined
            v-model="imageURL"
            type="text"
            label="Image URL"
          />
        </v-col>
        <v-col>
          <v-text-field
            outlined
            v-model="topText"
            type="text"
            label="Top Text"
          />
        </v-col>
        <v-col>
          <v-text-field
            outlined
            v-model="bottomText"
            type="text"
            label="Bottom Text"
          />
        </v-col>
      </v-row>
      <v-row v-if="!showMeme" justify="center">
        <v-btn :disabled="!imageURL" text color="primary" type="submit">
          Generate meme!
        </v-btn>
      </v-row>
    </v-form>

    <div v-if="showMeme">
      <div class="memeImageContainer">
        <meme
          class="memeImage"
          :top="topText"
          :bottom="bottomText"
          :imageURL="imageURL"
        />
      </div>
    </div>
    <div class="text-center mt-10 mb-10">
      <v-btn
        :disabled="!imageURL"
        type="button"
        @click="saveMeme"
        color="primary"
      >
        Save this meme
      </v-btn>
    </div>
  </v-container>
</template>

<script>
import Meme from "../components/Meme.vue";
import { db } from "../firebase";

export default {
  components: { Meme },
  data() {
    return {
      imageURL: "",
      topText: "",
      bottomText: "",
      showMeme: false,
    };
  },
  methods: {
    generateMeme() {
      this.showMeme = true;
    },
    async saveMeme() {
      await db.collection("memes").add({
        topText: this.topText,
        bottomText: this.bottomText,
        imageURL: this.imageURL,
        normalized: `${this.topText.toUpperCase()} ${this.bottomText.toUpperCase()}`,
      });

      this.$router.push("/feed");
    },
  },
};
</script>

<style scoped>
.memeForm {
  margin-top: 5em;
}

.memeImageContainer {
  display: flex;
  justify-content: center;
}

.test {
  font-size: 40pt;
  color: black;
}
</style>