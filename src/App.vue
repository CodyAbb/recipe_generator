<template>
  <div id="app">
    <h1>Recipe Fetcher</h1>

    <div class="component-container">
      <category-dropdown :categories="recipeCategories"/>
      <recipe-list :recipes="recipesFromCategory"/>
    </div>
  </div>
</template>

<script>
import {eventBus} from './main.js';

import RecipeCategoryDropdown from './components/RecipeCategoryDropdown.vue'
import RecipeList from './components/RecipeList.vue'

export default {
  name: 'app',
  data() {
    return{
      recipeCategories: [],
      searchCategoryTerm: "Beef",
      recipesFromCategory: []
    }
  },
  methods: {
    fetchRecipes(){
      let categoryUrl = `https://www.themealdb.com/api/json/v1/1/filter.php?c=${this.searchCategoryTerm}`
      fetch(categoryUrl)
        .then(req => req.json())
        .then(recipeArray => this.recipesFromCategory = recipeArray.meals)
    }
  },
  mounted(){
    fetch('https://www.themealdb.com/api/json/v1/1/categories.php')
      .then(req => req.json())
      .then(data => {
        const recipeCategories = data.categories.map(category => category.strCategory)
        this.recipeCategories = recipeCategories
      });

      this.fetchRecipes();



    eventBus.$on('category-selected', (category) => {
      this.searchCategoryTerm = category
    });
  },
  components: {
    "category-dropdown": RecipeCategoryDropdown,
    "recipe-list": RecipeList
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
