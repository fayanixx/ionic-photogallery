<template>
  <section class="gallery-card">
    <div class="gallery-header">
      <span class="gallery-pill">GALLERY</span>
      <span class="photo-counter">{{ photos.length }} PHOTOS</span>
    </div>

    <div v-if="photos.length === 0" class="empty-state">
      <div class="empty-icon-ring">
        <span>🎴</span>
      </div>
      <p class="empty-title">No photos yet!</p>
      <p class="empty-subtitle">Click the camera button to take one.</p>
    </div>

    <div v-else class="photos-grid">
      <div v-for="(photo, index) in photos" :key="index" class="photo-frame">
        <ion-img :src="photo" class="photo-img" />
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { IonImg } from "@ionic/vue";

defineProps<{
  photos: string[];
}>();
</script>

<style scoped>
.gallery-card {
  background: #141418;
  border-radius: 18px;
  border: 2px solid rgba(255, 182, 193, 0.18);
  padding: 18px;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.35);
}

.gallery-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
  padding-bottom: 12px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

.gallery-pill {
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 1.5px;
  color: #f7a8b8;
  background: rgba(247, 168, 184, 0.12);
  padding: 3px 10px;
  border-radius: 20px;
  border: 1px solid rgba(247, 168, 184, 0.25);
}

.photo-counter {
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 1px;
  color: #71717a;
}

.empty-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 42px 16px;
  text-align: center;
}

.empty-icon-ring {
  width: 58px;
  height: 58px;
  border-radius: 50%;
  background: #1a1a22;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  margin-bottom: 14px;
  border: 1px solid rgba(247, 168, 184, 0.2);
}

.empty-title {
  margin: 0;
  font-size: 0.95rem;
  font-weight: 600;
  color: #f4f4f5;
  letter-spacing: 0.5px;
}

.empty-subtitle {
  margin: 6px 0 0;
  font-size: 0.78rem;
  color: #71717a;
}

.photos-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 12px;
}

.photo-frame {
  aspect-ratio: 1 / 1;
  border-radius: 12px;
  overflow: hidden;
  border: 1px solid rgba(247, 168, 184, 0.2);
  background: #0d0d0f;
}

.photo-img {
  width: 100%;
  height: 100%;
}

.photo-img::part(image) {
  object-fit: cover;
}
</style>