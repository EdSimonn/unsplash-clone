<script>
export default {
  props: {
    image: Object,
  },
};
</script>

<template>
  <div class="image-card" @click="$emit('openModal', image)">
    <img :src="image.urls.small" :alt="image.alt_description" />
    <div class="overlay"></div>
    <div class="text">
      <p class="name">{{ image.user?.name || "Unknown" }}</p>
      <p class="location">{{ image.user?.location || "Unknown" }}</p>
    </div>
  </div>
</template>

<style lang="scss">
.image-card {
  position: relative;
  width: 100%;
  border-radius: 16px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;

  &:hover {
    transform: scale(1.05);
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
  }

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
    transition: transform 0.3s ease;
  }

  .overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.3);
    transition: background 0.3s ease;

    .image-card:hover & {
      background: rgba(0, 0, 0, 0.6);
    }
  }

  .text {
    position: absolute;
    bottom: 20px;
    left: 20px;
    color: white;
    font-size: 14px;
    font-family: "Google Sans", "Open Sans", "Roboto", sans-serif;
    text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.7);
    transition: transform 0.3s ease, opacity 0.3s ease;

    .image-card:hover & {
      transform: translateY(-5px);
      opacity: 1;
    }

    .name {
      font-size: 16px;
      color: white;
    }

    .location {
      font-size: 14px;
      opacity: 0.9;
      color: #ccc;
    }
  }
}
</style>
