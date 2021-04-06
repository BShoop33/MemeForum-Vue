<template>
  <div>
    <form>
      <input type="text" v-model="imageURL" />
      <input type="text" v-model="topText" />
      <input type="text" v-model="bottomText" />
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      imageURL: "",
      topText: "",
      bottomText: "",
    };
  },
};
</script>

<script>
export default {};
</script>

<style>
</style>