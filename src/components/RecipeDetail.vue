<template lang="html">
  <article v-if="recipe">
    <h3>{{ recipe.strMeal }}</h3>
    <img :src="recipe.strMealThumb" alt="Image Unavailable">
    <table>
      <tr>
        <td>{{recipe.strIngredient1}}</td>
        <td>{{recipe.strMeasure1}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient1}}</td>
        <td>{{recipe.strMeasure1}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient2}}</td>
        <td>{{recipe.strMeasure2}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient3}}</td>
        <td>{{recipe.strMeasure3}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient4}}</td>
        <td>{{recipe.strMeasure4}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient5}}</td>
        <td>{{recipe.strMeasure5}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient6}}</td>
        <td>{{recipe.strMeasure6}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient7}}</td>
        <td>{{recipe.strMeasure7}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient8}}</td>
        <td>{{recipe.strMeasure8}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient9}}</td>
        <td>{{recipe.strMeasure9}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient10}}</td>
        <td>{{recipe.strMeasure10}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient11}}</td>
        <td>{{recipe.strMeasure11}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient12}}</td>
        <td>{{recipe.strMeasure12}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient13}}</td>
        <td>{{recipe.strMeasure13}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient14}}</td>
        <td>{{recipe.strMeasure14}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient15}}</td>
        <td>{{recipe.strMeasure15}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient16}}</td>
        <td>{{recipe.strMeasure16}}</td>
      </tr><tr>
        <td>{{recipe.strIngredient17}}</td>
        <td>{{recipe.strMeasure17}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient18}}</td>
        <td>{{recipe.strMeasure18}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient19}}</td>
        <td>{{recipe.strMeasure19}}</td>
      </tr>
      <tr>
        <td>{{recipe.strIngredient20}}</td>
        <td>{{recipe.strMeasure20}}</td>
      </tr>
    </table>
    <p id="instructions">{{ recipe.strInstructions }}</p>
    <p>Original Source: <a :href="recipe.strSource">{{recipe.strSource}}</a></p>
  </article>
</template>

<script>
export default {
  name: 'recipe-detail',
  props: ['recipe']
}
</script>

<style lang="css" scoped>
h3{
  text-decoration: underline;
}

table:empty {
 display: none;
}

img{
  width: 500px;
}

td{
padding-left: 10px;
}

#instructions{
  padding-right: 30px;
}
</style>
