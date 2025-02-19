<template>
  <div v-if="!searchPerformed" class="search-container">
    <input
      type="text"
      v-model="searchQuery"
      @keyup.enter="emitSearch"
      placeholder="Search for photo"
    />
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

input {
  width: 90%;
  max-width: 1200px;
  padding: 15px 20px;
  border-radius: 12px;
  border: 1px solid #ccc;
  outline: none;
  font-size: 1.2rem;

  @media (max-width: 480px) {
    width: 80%;
  }
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
