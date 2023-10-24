<template>
    <div class="card-container">
      <div v-for="(item, index) in items.slice(0, 4)" :key="index" class="card">
        <img :src="item.image_url" alt="Animal" />
        <h3>{{ item.title }}</h3>
        <div class="rating-widget">
          <span v-for="n in item.rating" :key="n" class="star">★</span>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  
  export default {
    data() {
      return {
        items: [],
      };
    },
    mounted() {
      axios.get("images.json").then((response) => {
        this.items = response.data;
      });
    },
  };
  </script>

<style scoped>
.card-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.card {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  margin: 10px;
  text-align: center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  max-width: 250px; 
}

.card img {
  max-width: 100%;
}

.card h3 {
  margin: 10px 0;
  font-size: 1.5rem;
}

.rating-widget {
  font-size: 20px;
  color: #FFD700;
}

.star {
  display: inline-block;
  margin-right: 5px;
}
</style>
