<template>
    <div class="app">
    <div class="item-list">
      <div v-for="(item, index) in displayedItems" :key="index" class="item">
            <Tooltip :title="item.title" :rating="item.rating">
              <img :src="item.image_url" alt="Item Image">
            </Tooltip> 
            <h2>{{ item.title }}</h2>
            <div class="rating">
                <span class="star" v-for="n in item.rating" :key="n">★</span>
            </div>
      </div>
    </div>
      </div>
      <div class="pagination">
        <button @click="previousPage" :disabled="currentPage === 1">Previous</button>
        <span>Page {{ currentPage }} of {{ totalPages }}</span>
        <button @click="nextPage" :disabled="currentPage === totalPages">Next</button>
      </div>
    

</template>
  
  <script>
  import axios from "axios";
  import Tooltip from "./Tooltip.vue";
  import Photo from "./PhotoGalery.vue"
  
  export default {
    components: {
        Tooltip,
        Photo
    },
    data() {
      return {
        items: [],
        currentPage: 1,
        itemsPerPage: 4,
      };
    },
    mounted() {
      axios.get("images.json").then((response) => {
        this.items = response.data;
      });
    },
    computed: {
      totalPages() {
        return Math.ceil(this.items.length / this.itemsPerPage);
      },
      displayedItems() {
        const startIndex = (this.currentPage - 1) * this.itemsPerPage;
        const endIndex = startIndex + this.itemsPerPage;
        return this.items.slice(startIndex, endIndex);
      },
    },
    methods: {
      previousPage() {
        if (this.currentPage > 1) {
          this.currentPage--;
          this.scrollToTop();
        }
      },
      nextPage() {
        if (this.currentPage < this.totalPages) {
          this.currentPage++;
          this.scrollToTop();
        }
      },
      scrollToTop() {
        window.scrollTo(0, 0);
      },
    },
  };
  </script>
  
  <style>
  .app {
    text-align: center;
    font-family: Arial, sans-serif;
  }
  
  .item-list {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
  
  .item {
    border: 1px solid #ccc;
    margin: 50px 30px 10px 10px; 
    padding: 5px;
    text-align: center;
    max-width: 200px; 
  }
  
  img {
    max-width: 100%;
  }
  
  .pagination {
    margin-top: 20px;
  }
  
  button {
    margin: 0 10px;
    padding: 5px 10px;
  }
  
  .rating {
    font-size: 20px;
    margin-top: 10px;
  }
  
  .star {
    color: gold;
  }
  </style>
  
  
  