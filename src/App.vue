<template>
  <div class="app">
    <div class="auto-complete">
      <h1 class="text">AutoComplete</h1>
      <AutoComplete />
    </div>
    <div>
      <ImagesCarouselVue />
      <PhotoGalery/>
    </div>
    <div class="rating">
      <RatingWidget />
    </div>
    </div>
</template>


<script>
import AutoComplete from './components/AutoComplete.vue';
import ImagesCarouselVue from './components/ImagesCarousel.vue';
import RatingWidget from './components/RatingWidget.vue';
import Tooltip from './components/Tooltip.vue';
import PhotoGalery from './components/PhotoGalery.vue';
  export default {
    components: {
    AutoComplete,
    ImagesCarouselVue,
    Tooltip,
    RatingWidget,
    PhotoGalery,
}
  }
</script>

<style scoped>


.app {
  background-color: azure;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
}
.auto-complete {
  max-height: 150px;
  /* overflow-y: auto; */
  /* display: flex; */
  flex-direction: column;
  align-items: center;
  justify-content: center;

}
.image-carousel {
  flex-grow: 1; 
  top: 50px;
  text-align: center;
  display: flex;
  flex-direction: column;

}
.tooltip{
  position: absolute;
  top: 100%;
  left: 80px;
  right: 75px;
  background-color: #FFF;
  border: 1px solid #CCC;
  padding: 10px;
  border-radius: 5px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
  z-index: 999;
  justify-content: center;
  align-items: center;
  justify-items: center;
  margin-top: 10px;
}
.photo-gallery {
  position: relative;
  margin-top: 20px;
}
</style>
