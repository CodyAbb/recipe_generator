<template>
  <div id="app">


    <div class="component-container">
      <div class="header-container">
        <h1 id="title" class="title">Recipe Fetcher</h1>
        <h3>Have a look for some culinary inspiration...</h3>
      </div>

      <category-dropdown id="recipe-category-list" :categories="recipeCategories"/>
      <recipe-list id="recipe-list" :recipes="recipesFromCategory"/>
      <recipe-detail id="recipe-info" :recipe="selectedRecipe"/>
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
      searchCategoryTerm: "",
      recipesFromCategory: [],
      selectedRecipeId: null,
      selectedRecipe: null
    }
  },
  watch: {
   // whenever question changes, this function will run
   searchCategoryTerm: function () {
     this.fetchRecipes();
   },
   selectedRecipeId: function(){
     this.fetchChosenRecipe();
   }
 },
  methods: {
    fetchRecipes(){
      // let categoryUrl = `https://www.themealdb.com/api/json/v1/1/filter.php?c=Beef`

      let categoryUrl = `https://www.themealdb.com/api/json/v1/1/filter.php?c=${this.searchCategoryTerm}`
      fetch(categoryUrl)
        .then(req => req.json())
        .then(recipeArray => this.recipesFromCategory = recipeArray.meals)
    },
    fetchChosenRecipe(){
      let recipeUrl = `https://www.themealdb.com/api/json/v1/1/lookup.php?i=${this.selectedRecipeId}`
      fetch(recipeUrl)
        .then(req => req.json())
        .then(data=> data.meals[0])
        .then(recipe => this.selectedRecipe = recipe)
        // .then(recipe => this.selectedRecipe = recipe.meals)
    }
  },
  mounted(){


    fetch('https://www.themealdb.com/api/json/v1/1/categories.php')
      .then(req => req.json())
      .then(data => {
        const recipeCategories = data.categories.map(category => category.strCategory)
        this.recipeCategories = recipeCategories
      });




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
#app {
  font-family: 'Merriweather', serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {

}

.header-container {
  grid-area: header;
  justify-self: start;
  font-weight: 700;
  font-size: 2em;
}
#recipe-category-list {
  grid-area: filter;
  justify-self: left;
  align-self: center;
}
#recipe-list {
  grid-area: list;
  justify-self: left;
}
#recipe-info {
  grid-area: article;
}

.component-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: auto;
  grid-template-areas:
    "header header filter"
    "list article article";
}
</style>
