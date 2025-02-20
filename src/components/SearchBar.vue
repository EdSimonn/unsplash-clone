<template>
  <div v-if="!searchPerformed" class="search-container">
    <div class="input-wrapper">
      <svg
        @click="emitSearch"
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round"
        class="search-icon"
      >
        <circle cx="11" cy="11" r="8"></circle>
        <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
      </svg>
      <input
        type="text"
        v-model="searchQuery"
        @keyup.enter="emitSearch"
        placeholder="Search for photo"
      />
    </div>
  </div>
  <div v-else class="search-results">
    Search Results for <span class="highlight">"{{ searchQuery }}"</span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: "",
      searchPerformed: false,
    };
  },
  methods: {
    emitSearch() {
      if (this.searchQuery.trim()) {
        this.searchPerformed = true;
        this.$emit("search", this.searchQuery);
      }
    },
  },
};
</script>

<style lang="scss">
.search-container {
  background: #e3e8f0;
  display: flex;
  justify-content: center;
  padding: 6rem 0;
  padding-bottom: 7rem;
  margin: 0;
  overflow-x: hidden;
}

.input-wrapper {
  display: flex;
  align-items: center;
  position: relative;
  width: 90%;
  max-width: 1200px;
  background: white;
  border-radius: 12px;
  border: 1px solid #ccc;
  padding: 10px;
}

.search-icon {
  flex-shrink: 0;
  margin-right: 10px;
  color: #64748b;
  cursor: pointer;
  transition: color 0.2s ease-in-out;
}

.search-icon:hover {
  color: #1e293b;
}

input {
  flex: 1;
  padding: 12px 15px;
  border: none;
  outline: none;
  font-size: 1.2rem;
  width: 100%;
  background: transparent;
}

.search-results {
  background: #e3e8f0;
  padding: 5rem 0;
  text-align: left;
  padding-left: 5%;
  font-size: 2rem;
  font-weight: bold;
  color: #1e293b;
}

.highlight {
  color: #64748b;
  font-style: italic;
}
</style>
