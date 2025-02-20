<template>
  <div class="modal-overlay" @click.self="close">
    <div class="modal-content">
      <button class="close-btn" @click="close">×</button>
      <img
        :src="image.urls.regular"
        :alt="image.alt_description"
        class="modal-image"
      />
      <div class="modal-info">
        <h2>{{ image.user?.name || "Unknown" }}</h2>
        <p class="location">{{ image.user?.location || "Unknown" }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    image: Object,
  },
  methods: {
    close() {
      this.$emit("close");
    },
  },
};
</script>

<style lang="scss">
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  background: white;
  border-radius: 10px;
  overflow: hidden;
  max-width: 800px;
  width: 90%;
  display: flex;
  flex-direction: column;
  position: relative;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
}

.close-btn {
  position: absolute;
  top: 10px;
  right: 15px;
  font-size: 24px;
  border: none;
  background: none;
  cursor: pointer;
  color: white;
  z-index: 10;
}

.modal-image {
  width: 100%;
  max-height: 500px;
  object-fit: cover;
}

.modal-info {
  padding: 20px;
  background: white;
  text-align: left;
  font-size: 18px;
  color: black;
  border-top: 1px solid #ddd;
}

h2 {
  margin: 0;
  font-size: 20px;
  font-weight: bold;
}

p {
  margin: 5px 0 0;
  color: #666;
  font-size: 16px;
}
</style>
