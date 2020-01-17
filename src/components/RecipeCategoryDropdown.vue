<template lang="html">
  <div class="dropdown-list">
    <form v-on:submit.prevent>
      <label for="category-select">Pick a category: </label>
      <select id="category-select" v-on:change="handleChange" v-model="selectedCategory">
         <option v-for="category in categories" :value="category">{{category}}</option>
       </select>
    </form>
  </div>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  data (){
    return{
        "selectedCategory": ""
    }

  },
  props: ['categories'],
  methods: {
    handleChange(){
      eventBus.$emit('category-selected', this.selectedCategory)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
