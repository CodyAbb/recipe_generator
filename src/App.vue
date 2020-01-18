<template>
  <div id="app">
    <h1>Recipe Fetcher</h1>

    <div class="component-container">
      <category-dropdown :categories="recipeCategories"/>
      <recipe-list :recipes="recipesFromCategory"/>
      <recipe-detail :recipe="renderedRecipe"/>
    </div>
  </div>
</template>

<script>
import {eventBus} from './main.js';

import RecipeCategoryDropdown from './components/RecipeCategoryDropdown.vue'
import RecipeList from './components/RecipeList.vue'
import RecipeDetail from './components/RecipeDetail.vue'

export default {
  name: 'app',
  data() {
    return{
      recipeCategories: [],
      searchCategoryTerm: "Beef",
      recipesFromCategory: [],
      selectedRecipeId: null
    }
  },
  methods: {
    fetchRecipes(){
      // let categoryUrl = `https://www.themealdb.com/api/json/v1/1/filter.php?c=Beef`

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

    eventBus.$on('recipe-selected', (recipeId) => {
     this.selectedRecipeId = recipeId
   });
  },
  components: {
    "category-dropdown": RecipeCategoryDropdown,
    "recipe-list": RecipeList,
    "recipe-detail": RecipeDetail
  },
  computed: {
    renderedRecipe: function() {
      return this.recipesFromCategory.find(recipe => recipe.idMeal === this.selectedRecipeId)
    }
  }

}
</script>

<style>

</style>
