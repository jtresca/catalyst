<template>
  <div class="search-container">
    <input v-on:input="(event) => this.$emit('inputChange',event)" placeholder="Search Logos...">
  </div>
</template>

<script>
export default {
  name: "LogoSearch",
  props: ["suggest"],
  methods: {
    addItem() {
      console.log("ITEM ADDED");
    }
  }
  
}
</script>

<style scoped>
 
</style>