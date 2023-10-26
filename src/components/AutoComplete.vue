<template>
  <div class="nav">
    <input
      v-model="userInput"
      @input="filterSuggestions"
      @click="filterSuggestions"
      placeholder="Pencarian"
    />
    <ul v-if="userInput && showSuggestionsList" class="suggestions">
      <li v-for="suggestion in filteredSuggestions" :key="suggestion.title" @click="selectSuggestion(suggestion)">
        {{ suggestion.title }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      userInput: '',
      suggestions: [],
      showSuggestionsList: false,
    };
  },
  computed: {
    filteredSuggestions() {
      return this.suggestions.filter((suggestion) =>
        suggestion.title.toLowerCase().includes(this.userInput.toLowerCase())
      );
    },
  },
  methods: {
    async fetchData() {
      try {
        const response = await axios.get('images.json'); 
        this.suggestions = response.data;
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },
    filterSuggestions() {
      if (this.userInput !== '') {
        this.showSuggestionsList = true;
      } else {
        this.showSuggestionsList = false;
      }
    },
    selectSuggestion(suggestion) {
      this.userInput = suggestion.title;
      this.showSuggestionsList = false;
    },
  },
  mounted() {
    this.fetchData();
  },
};
</script>

<style scoped>

.suggestions {
  position: absolute;
  border: 1px solid #ccc;
  background: white;
  max-height: 150px;
  overflow-y: auto;
  width: 100%;
  margin-top: 5px;
  border-radius: 4px; 
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); 
  z-index: 1; 
}

input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  font-size: 16px;
  margin-bottom: 5px;
}

li {
  padding: 10px;
  cursor: pointer;
}

li:hover {
  background-color: #f0f0f0;
}
</style>
