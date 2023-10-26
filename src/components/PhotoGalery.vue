<template>
  <div>
    <div class="image-gallery">
      <div class="lightbox-content">
        <div v-for="(item, index) in jsonData" :key="index">
          <div class="gallery-item" @click="openLightbox(item)">
            <img :src="item.image_url" alt="Gambar" class="lightbox-trigger" />
          </div>
        </div>
      </div>
    </div>

    <div v-if="showLightbox" class="lightbox-modal" @click="closeLightbox">
      <div class="lightbox-content">
        <span class="close-button">×</span>
        <img :src="lightboxImage" alt="Gambar Lightbox" class="lightbox-image" />
      </div>
    </div>
  </div>
</template>
<style>
.image-gallery {
  display: flex;
  max-width: 100%;
  align-items: flex-end; 
  margin-top: 50px;
  justify-content: center; 
  overflow-x: auto;
}

.lightbox-content {
  display: flex;
  align-items: center;
  overflow: auto;
}

.gallery-item {
  cursor: pointer;
  max-width: 200px;
  margin-right: 10px; 
}

.lightbox-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
}

.lightbox-content {
  position: relative;
}

.close-button {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 24px;
  cursor: pointer;
  color: white;
}

.lightbox-image {
  max-width: 80%;
  max-height: 80%;
}

@media (max-width: 768px) {
  .image-gallery {
    flex-direction: column;
    align-items: center;
    margin-top: 20px;
  }

  .gallery-item {
    max-width: 100%;
    margin-right: 0;
    margin-bottom: 20px;
  }

  .lightbox-content {
    align-items: center;
    text-align: center;
  }
}


</style>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      jsonData: [],
      showLightbox: false,
      lightboxImage: '',
    };
  },
  mounted() {
    axios.get('images.json')
      .then(response => {
        this.jsonData = response.data.slice(0, 5);
      })
      .catch(error => {
        console.error('Gagal mengambil data: ' + error);
      });
  },
  methods: {
    openLightbox(item) {
      this.showLightbox = true;
      this.lightboxImage = item.image_url;
    },
    closeLightbox() {
      this.showLightbox = false;
      this.lightboxImage = '';
    },
  },
};
</script>
