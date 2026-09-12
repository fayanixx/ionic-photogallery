<template>
  <ion-page>
    <ion-header class="ion-no-border">
      <ion-toolbar class="custom-toolbar">
        <ion-title class="gallery-title">
          MY PHOTO <span>GALLERY</span>
        </ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" class="custom-content">
      <main class="page-container">
        <CameraComponent @photoCaptured="addPhoto" />

        <PhotoGalleryComponent :photos="photos" />
      </main>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
} from "@ionic/vue";
import { ref } from "vue";
import CameraComponent from "@/components/CameraComponent.vue";
import PhotoGalleryComponent from "@/components/PhotoGalleryComponent.vue";

const photos = ref<string[]>([]);

const addPhoto = (photoPath: string) => {
  photos.value.unshift(photoPath);
};
</script>

<style scoped>
.custom-toolbar {
  --background: #0d0d0f;
  border-bottom: 3px solid rgba(255, 182, 193, 0.12);
  padding: 8px 12px;
}

.gallery-title {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  font-size: 1.15rem;
  font-weight: 800;
  letter-spacing: 2px;
  color: #ffffff;
}

.gallery-title span {
  color: #f7a8b8;
}

.custom-content {
  --background: #0d0d0f;
}

.page-container {
  max-width: 540px;
  margin: 0 auto;
  padding: 16px 14px 40px;
  display: flex;
  flex-direction: column;
  gap: 18px;
}
</style>