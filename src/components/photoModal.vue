<template>
  <div class="modal-background" @click.self="close">
    <div class="modal-content">
      <img :src="photo.urls.full" :alt="photo.alt_description" />
      <div class="modal-caption">
        <p>{{ photo.user.name }} - {{ photo.location?.name || 'Unknown location' }}</p>
      </div>
      <button class="close-btn" @click="close">Close</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['photo'],
  methods: {
    close() {
      this.$emit('close'); // Emit close event to parent
    },
  },
};
</script>

<style scoped>
.modal-background {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.75);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 8px;
  max-width: 80%;
  max-height: 80%;
  overflow: auto;
}

.modal-content img {
  max-width: 100%;
  border-radius: 8px;
}

.modal-caption {
  margin-top: 10px;
  text-align: center;
}

.close-btn {
  margin-top: 10px;
  background-color: #333;
  color: white;
  padding: 8px 16px;
  border: none;
  cursor: pointer;
  border-radius: 4px;
}
</style>
