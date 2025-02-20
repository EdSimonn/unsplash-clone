<template>
  <div class="image-grid">
    <div v-if="loading" class="placeholder-grid">
      <div
        class="placeholder"
        v-for="(image, index) in images"
        :key="index"
        :class="`grid-item grid-row-${(index % 3) + 1}`"
      >
        <div class="shimmer"></div>
        <div class="placeholder-text">
          <div class="line"></div>
          <div class="line short"></div>
        </div>
      </div>
    </div>
    <div v-else class="grid">
      <ImageCard
        v-for="(image, index) in images"
        :key="image.id"
        :image="image"
        :class="`grid-item grid-row-${(index % 3) + 1}`"
        @openModal="openModal"
      />
    </div>

    <ImageModal
      v-if="selectedImage"
      :image="selectedImage"
      @close="selectedImage = null"
    />
  </div>
</template>

<script>
import ImageCard from "./ImageCard.vue";
import ImageModal from "./ImageModal.vue";

export default {
  components: { ImageCard, ImageModal },
  props: {
    images: Array,
    loading: Boolean,
  },
  data() {
    return {
      selectedImage: null,
    };
  },
  methods: {
    openModal(image) {
      this.selectedImage = image;
    },
  },
};
</script>

<style lang="scss">
.image-grid {
  max-width: 1200px;
  margin: auto;
  padding: 0rem 8rem;
  padding-bottom: 3rem;
  margin-top: -50px;

  @media (max-width: 834px) {
    padding: 0rem 2rem;
  }
}

.grid,
.placeholder-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 250px;
  gap: 40px;

  @media (max-width: 1024px) {
    grid-template-columns: repeat(2, 1fr);
  }

  @media (max-width: 768px) {
    grid-template-columns: repeat(1, 1fr);
  }
}

.placeholder {
  background-color: #f3f3f3;
  border-radius: 12px;
  position: relative;
  overflow: hidden;
  display: flex;
  align-items: flex-end;
  justify-content: flex-start;
  padding: 10px;

  &.grid-row-1 {
    grid-row: span 1;
  }

  &.grid-row-2 {
    grid-row: span 2;
  }

  &.grid-row-3 {
    grid-row: span 3;
  }

  &::after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 25%;
    height: 100%;
    background: linear-gradient(
      to right,
      #f3f3f3 0%,
      #e0e0e0 50%,
      #f3f3f3 100%
    );
    animation: shimmer 1.5s infinite linear;
  }
}

.placeholder-text {
  position: absolute;
  bottom: 10px;
  left: 10px;
  display: flex;
  flex-direction: column;
  gap: 5px;
  z-index: 2;
  width: 60%;
}

.placeholder-text .line {
  height: 10px;
  background: #e0e0e0;
  border-radius: 4px;
  width: 100%;
}

.placeholder-text .short {
  width: 60%;
}

.grid-item {
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  border-radius: 12px;
}

.grid-row-1 {
  grid-row: span 1;
}

.grid-row-2 {
  grid-row: span 2;
}

.grid-row-3 {
  grid-row: span 3;
}

@keyframes shimmer {
  0% {
    left: -100%;
  }
  100% {
    left: 100%;
  }
}
</style>
