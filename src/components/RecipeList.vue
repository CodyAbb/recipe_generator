<template lang="html">
  <div class="recipes-container">
    <ul>
      <li v-for="recipe in recipes">{{recipe.strMeal}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props:['recipes']
}
</script>

<style lang="css" scoped>
</style>
