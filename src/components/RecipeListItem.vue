<template lang="html">
<li class="pointer" v-on:click="handleClick">{{recipe.strMeal}}</li>
</template>

<script>
import {eventBus} from '../main.js'

export default {
name: 'recipe-list-item',
props: ['recipe'],
methods: {
  handleClick(){
    eventBus.$emit('recipe-selected', this.recipe.idMeal)
  }
}
}
</script>

<style lang="css" scoped>
li .pointer {
  cursor: pointer;
}
</style>
