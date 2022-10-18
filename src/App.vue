<template>
  <div id="app">
    <div v-for="gif in gifs" :key="gif[0]">
      <img :src="gif[1]" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",

  data() {
    return {
      gifs: [],
    };
  },

  mounted() {
    // FIX THE REQUEST URL WITH MODES
    axios
      .request({
        url: "http://localhost:5000/api/gifs",
      })
      .then((res) => {
        this.gifs = res["data"];
      })
      .catch(() => {});
  },
};
</script>

<style>
img {
  max-width: 100%;
  object-fit: cover;
}

#app {
  display: grid;
  place-items: center;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}
</style>
