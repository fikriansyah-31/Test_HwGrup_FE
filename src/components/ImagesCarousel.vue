<template>
    <div class="image-carousel">
      <div class="carousel-content">
        <button @click="moveSlide(-1)" class="carousel-button prev">&#8249;</button>
        <div v-for="(image, index) in visibleImages" :key="index" class="carousel-slide">
          <img :src="image.image_url" :alt="image.title" class="carousel-image" />
        </div>
        <button @click="moveSlide(1)" class="carousel-button next">&#8250;</button>
      </div>
    </div>
  </template>
  
  <style scoped>
  .image-carousel {
    text-align: center;
    position: relative;
    
  }
  
  .carousel-content {
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }
  
  .carousel-slide {
    max-width: 33.33%; 
    text-align: center;
    display: inline-block;
    padding: 10px;
    box-sizing: border-box;
  }
  
  .carousel-button {
    cursor: pointer;
    padding: 10px 20px;
    color: white;
    border: none;
    border-radius: 5px;
    margin: 0 10px;
  }
  
  .carousel-image {
  max-width: 80%; 
  max-height: 90%; 
}

.prev {
    order: -1;
}

@media (max-width: 768px) {
  .carousel-slide {
    max-width: 50%; 
  }
}

@media (max-width: 480px) {
  .carousel-slide {
    max-width: 100%; 
  }
}
  </style>
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        images: [],
        currentIndex: 0,
        slidesToShow: 3, 
      };
    },
    mounted() {
      axios.get('images.json')
        .then((response) => {
          this.images = response.data;
        })
        .catch((error) => {
          console.error('Gagal mengambil data gambar:', error);
        });
    },
    computed: {
      visibleImages() {
        const start = this.currentIndex;
        const end = start + this.slidesToShow;
        return this.images.slice(start, end);
      },
    },
    methods: {
      moveSlide(step) {
        const totalImages = this.images.length;
        this.currentIndex = (this.currentIndex + step + totalImages) % totalImages;
      },
    },
  };
  </script>
  
  