<template>
  <div id="app">
    <h1>Recipe Fetcher</h1>

    <div class="component-container">
      <category-dropdown :categories="recipeCategories"/>
    </div>
  </div>
</template>

<script>
import {eventBus} from './main.js';

import MealCategoryDropdown from './components/MealCategoryDropdown.vue'

export default {
  name: 'app',
  data() {
    return{
      recipeCategories: []
    }
  },
  mounted(){
    fetch('https://www.themealdb.com/api/json/v1/1/categories.php')
      .then(req => req.json())
      .then(data => {
        const recipeCategories = data.categories.map(category => category.strCategory)
        this.recipeCategories = recipeCategories
      })
  },
  components: {
    "category-dropdown": MealCategoryDropdown
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
