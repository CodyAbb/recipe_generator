<template lang="html">
  <div class="recipes-container">
    <ul>
      <recipe-list-item id="pointer-hover"v-for="recipe in recipes" :recipe="recipe"></recipe-list-item>
    </ul>
  </div>
</template>

<script>
import RecipeListItem from './RecipeListItem.vue'

export default {
  props:['recipes'],
  components: {
    "recipe-list-item": RecipeListItem
  }
}
</script>

<style lang="css" scoped>
#pointer-hover:hover{
cursor: pointer;
}

.recipes-container{
  border-radius: 15px;
  background-color: #586BA4;
  color: white;
}
</style>
