<template>
  <div>
    <!-- Photo Grid -->
    <div v-if="photos.length > 0" class="photo-grid">
      <div
        v-for="photo in photos"
        :key="photo.id"
        class="photo-item"
        @click="openModal(photo)"
      >
        <img :src="photo.urls.small" :alt="photo.alt_description" />
        <div class="overlay">
          <p>{{ photo.user.name }} - {{ photo.location?.name || 'Unknown location' }}</p>
        </div>
      </div>
    </div>

    <!-- Loading State Placeholder -->
    <div v-if="isLoading" class="loading-placeholder">
      <div v-for="n in 8" :key="n" class="placeholder-box"></div>
    </div>

    <!-- Modal for Full-Resolution Image -->
    <photoModal v-if="selectedPhoto" :photo="selectedPhoto" @close="closeModal" />
  </div>
</template>

<script>
import photoModal from './photoModal.vue';

export default {
  components: {
    photoModal,
  },
  props: ['photos', 'loading'],
  data() {
    return {
      selectedPhoto: null,
    };
  },
  methods: {
    openModal(photo) {
      this.selectedPhoto = photo; // Set selected photo to open the modal
    },
    closeModal() {
      this.selectedPhoto = null; // Clear selected photo to close the modal
    },
  },
};


</script>

<style scoped>
.photo-grid {
  display: grid;
  width: 50%;
  margin: 0 auto;
  align-self: center;
  justify-self: center;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
  margin-top: -50px; /* Adjust for overlap with the search bar */
}

.photo-item {
  position: relative;
  overflow: hidden;
  border-radius: 8px;
  cursor: pointer; /* Pointer cursor for clickable items */
}

.photo-item img {
  width: 100%;
  height: auto;
  display: block;
  object-fit: cover; /* Ensure images do not stretch */
}

.overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.5); /* Tint overlay for text contrast */
  color: white;
  padding: 10px;
  text-align: center;
}

/* Loading State */
.loading-placeholder {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
}

.placeholder-box {
  height: 250px;
  background-color: #ddd;
  border-radius: 8px;
  animation: pulse 1.5s infinite;
}

@keyframes pulse {
  0% {
    background-color: #ddd;
  }
  50% {
    background-color: #ccc;
  }
  100% {
    background-color: #ddd;
  }
}
</style>
