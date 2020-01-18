<template lang="html">
  <article v-if="recipe">
    <h3>{{ recipe.strMeal }}</h3>
    <img :src="recipe.strMealThumb" alt="Image Unavailable">
    <table>
      <tr>
        <td>{{recipe.strIngredient1}}</td>
        <td>{{recipe.strMeasure1}}</td>
      </tr>
    </table>
  </article>
</template>

<script>
export default {
  name: 'recipe-detail',
  props: ['recipe']
}
</script>

<style lang="css" scoped>
table{
  width: 100%;
}
</style>
