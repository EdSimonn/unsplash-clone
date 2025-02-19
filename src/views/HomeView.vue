<script>
import SearchBar from "@/components/SearchBar.vue";
import ImageGrid from "@/components/ImageGrid.vue";
import axios from "axios";

export default {
  components: { SearchBar, ImageGrid },
  data() {
    return {
      images: [],
      loading: true,
    };
  },
  methods: {
    async fetchImages(query = "") {
      this.loading = true;
      try {
        const response = await axios.get(
          `https://api.unsplash.com/search/photos`,
          {
            params: { query, per_page: 20 },
            headers: {
              Authorization: `Client-ID ${import.meta.env.VITE_UNSPLASH_ACCESS_KEY}`,
            },
          }
        );

        console.log("API Response:", response.data);

        this.images = response.data.results || [];
      } catch (error) {
        console.error("Error fetching images:", error);
      } finally {
        this.loading = false;
      }
    },
  },
  mounted() {
    this.fetchImages("african people");
  },
};
</script>

<template>
  <div class="">
    <SearchBar @search="fetchImages" />
    <ImageGrid :images="images" :loading="loading" />
  </div>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
}
.landing-page {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  overflow-x: hidden;
  padding: 0;
  margin: 0 auto;
  top: 0;
  left: 0;
}
</style>
