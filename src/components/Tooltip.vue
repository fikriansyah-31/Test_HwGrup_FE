<template>
    <div @mouseenter="showTooltip" @mouseleave="hideTooltip" class="tooltip">
      <slot></slot>
      <div v-if="visible" class="tooltiptext">
        {{ title }} - Rating: {{ rating }}
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      title: String,
      rating: Number,
    },
    data() {
      return {
        visible: false,
      };
    },
    methods: {
      showTooltip() {
        this.visible = true;
      },
      hideTooltip() {
        this.visible = false;
      },
    },
  };
  </script>
  
  <style scoped>
  .tooltip {
    position: relative;
    display: inline-block;
    cursor: pointer;
  }
  
  .tooltip .tooltiptext {
    visibility: hidden;
    width: 120px;
    background-color: #7d7878;
    color: #fff;
    text-align: center;
    border-radius: 6px;
    padding: 5px;
    position: absolute;
    z-index: 1;
    bottom: 12%; 
    left: 100%;
    transform: translateX(-50%);
    opacity: 0;
    transition: opacity 0.3s;
  }
  
  .tooltip:hover .tooltiptext {
    visibility: visible;
    opacity: 1;
  }
  </style>
  