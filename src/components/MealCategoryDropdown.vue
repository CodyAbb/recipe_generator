<template lang="html">
  <div class="dropdown-list">
    <label for="category-select">Pick a category</label>
    <select id="category-select">
      <option default selected value></option>
       <option v-for="category in categories" :value="category">{{category}}</option>
     </select>

    </select>
  </div>
</template>

<script>
export default {
  props: ['categories']
}
</script>

<style lang="css" scoped>
</style>
