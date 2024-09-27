<template>
  <div id="app">
    <!-- Search Bar -->
    <header class="search-bar">
      <input
        type="text"
        v-model="searchQuery"
        @keyup.enter="searchPhotos"
        placeholder="Search Unsplash"
      />
    </header>

    <photoGrid :photos="photos" :loading="loading" />
  </div>
</template>

<script>
import photoGrid from './components/photoGrid.vue';
import axios from 'axios';

export default {
  components: {
    photoGrid,
  },
  data() {
    return {
      searchQuery: 'african',
      photos: [],
      loading: false,
    };
  },
  methods: {
    async searchPhotos() {
      this.loading = true;
      try {
        const response = await axios.get('https://api.unsplash.com/search/photos', {
          params: {
            query: this.searchQuery,
            client_id: import.meta.env.VITE_UNSPLASH_ACCESS_KEY,
            per_page: 8,
          },
        });
        this.photos = response.data.results;
      } catch (error) {
        console.error('Error fetching photos:', error);
      } finally {
        this.loading = false;
      }
    },
  },
  mounted() {
    this.searchPhotos(); // Fetch default photos on mount
  },
};
</script>

<style scoped>
.search-bar {
  background-color: #f8f8f8;
  padding: 50px;
  text-align: center;
  margin-bottom: 20px;
}

.search-bar input {
  width: 300px;
  padding: 10px;
  border-radius: 25px;
  border: 1px solid #ddd;
  outline: none;
}

.search-bar input:focus {
  border-color: #aaa;
}
</style>
