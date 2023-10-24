<template>
    <div>
      <div class="image-list">
        <div
          v-for="(item, index) in jsonData.slice(0, 10)"
          :key="index"
          class="image-container"
        >
          <img
            :src="item.image_url"
            alt="Image"
            @mouseover="showTooltip(item)"
            @mouseleave="hideTooltip(item)"
          />
          <div class="tooltip" :class="{ active: item.showTooltip }">
            <div class="tooltip-content">
              <p><strong>Title:</strong> {{ item.title }}</p>
              <p><strong>Rating:</strong> {{ item.rating }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  
  export default {
    data() {
      return {
        jsonData: [],
      };
    },
    mounted() {
      this.fetchData();
    },
    methods: {
      async fetchData() {
        try {
          const response = await axios.get("images.json");
          this.jsonData = response.data;
  
          this.jsonData.forEach((item) => {
            item.showTooltip = false;
          });
        } catch (error) {
          console.error("Error fetching data:", error);
        }
      },
      showTooltip(item) {
        item.showTooltip = true;
      },
      hideTooltip(item) {
        item.showTooltip = false;
      },
    },
  };
  </script>
  
  <style scoped>
  .image-list {
    display: flex;
  }
  
  .image-container {
    margin: 10px;
    text-align: center;
    position: relative;
  }
  
  .tooltip {
    display: none;
    position: absolute;
    background: #942a2a;
    border: 1px solid #ccc;
    padding: 10px;
    border-radius: 5px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
    z-index: 999;
    top: 0;
    left: 50%;
    transform: translate(-50%, -100%);
    color: #fff;
  }
  
  .tooltip.active {
    display: block;
  }
  
  .tooltip-content {
    text-align: left;
  }
  
  .tooltip img {
    max-width: 100px;
  }
  </style>
  