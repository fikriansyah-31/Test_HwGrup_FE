<template>
    <div class="photo-gallery">
      <div v-for="(photo, index) in mainPhotos" :key="index" class="main-photo">
        <img :src="photo.image_url" :alt="photo.title" @click="openLightbox(index)" />
      </div>
  
      <div class="lightbox" v-if="lightboxOpen">
        <span class="close-button" @click="closeLightbox">×</span>
        <img :src="photos[currentPhotoIndex].image_url" :alt="photos[currentPhotoIndex].title" />
      </div>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  
  export default {
    data() {
      return {
        photos: [],
        mainPhotos: [],
        lightboxOpen: false,
        currentPhotoIndex: 0,
      };
    },
    created() {
      axios.get('images.json')
        .then((response) => {
          this.photos = response.data;
          this.mainPhotos = this.photos.slice(0, 6);
        })
        .catch((error) => {
          console.error("Terjadi kesalahan saat mengambil data foto:", error);
        });
    },
    methods: {
      openLightbox(index) {
        this.currentPhotoIndex = index;
        this.lightboxOpen = true;
      },
      closeLightbox() {
        this.lightboxOpen = false;
      },
    },
  };
  </script>
  
  <style scoped>
  .photo-gallery {
    display: flex;
    flex-wrap: wrap;
  }
  
  .main-photo {
    flex: 1;
    margin: 10px;
    text-align: center;
    cursor: pointer;
  }
  
  .main-photo img {
    max-width: 100%;
    height: auto;
  }
  
  .lightbox {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.7);
  }
  
  .lightbox img {
    max-width: 90%;
    max-height: 90%;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
  
  .close-button {
    position: absolute;
    top: 10px;
    right: 10px;
    font-size: 24px;
    color: white;
    cursor: pointer;
  }
  </style>
  