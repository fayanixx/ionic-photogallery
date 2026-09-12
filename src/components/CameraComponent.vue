<template>
  <div class="camera-wrapper">
    <button type="button" class="btn-capture" @click="takePicture">
      <ion-icon :icon="cameraIcon" class="btn-icon" />
      <span>TAKE PICTURE</span>
    </button>

    <div v-if="errorMessage" class="error-badge">
      {{ errorMessage }}
    </div>
  </div>
</template>

<script setup lang="ts">
import { IonIcon } from "@ionic/vue";
import { camera as cameraIcon } from "ionicons/icons";
import { Camera, CameraResultType } from "@capacitor/camera";
import { ref } from "vue";

const errorMessage = ref("");
const emit = defineEmits<{
  (event: "photoCaptured", photo: string): void;
}>();

const takePicture = async () => {
  errorMessage.value = "";
  try {
    const photo = await Camera.getPhoto({
      quality: 90,
      resultType: CameraResultType.Uri,
      saveToGallery: false,
    });
    if (photo.webPath) {
      emit("photoCaptured", photo.webPath);
    }
  } catch (error) {
    console.error(error);
    errorMessage.value = "Unable to capture photo.";
  }
};
</script>

<style scoped>
.camera-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}

.btn-capture {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  background: #141418;
  color: #f7a8b8;
  border: 1.5px solid #f7a8b8;
  border-radius: 14px;
  padding: 16px 20px;
  font-size: 0.88rem;
  font-weight: 700;
  letter-spacing: 1.5px;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
  box-shadow: 0 4px 18px rgba(247, 168, 184, 0.12);
}

.btn-capture:active {
  transform: scale(0.98);
  background: #f7a8b8;
  color: #0d0d0f;
}

.btn-icon {
  font-size: 1.25rem;
}

.error-badge {
  font-size: 0.78rem;
  color: #ff6b81;
  background: rgba(255, 107, 129, 0.1);
  padding: 6px 14px;
  border-radius: 8px;
  border: 1px solid rgba(255, 107, 129, 0.25);
}
</style>