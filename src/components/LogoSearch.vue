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
  .search-container {
    width: 100%;
    text-align: center;
    margin: auto;
    padding-top: 1em;
  }

  input {
    width: 200px;
    padding: .5em;
    font-size: 1em;
    margin: auto;
    border: none;
  }
</style>