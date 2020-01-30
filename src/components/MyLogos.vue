<template>
  <div class="store-container">
    <ul  v-bind:key="logoItem.id" v-for="logoItem in logoStore">
      <li class="logo-item"><img :src="logoItem.logo" height="60" width="60"><span>{{logoItem.name}}</span><button @click="deleteItem(logoItem)">+</button></li> 
    </ul>
  </div>
</template>

<script>
export default {
  name: "MyLogos",
  props: ["logoStore"],
  methods: {
    deleteItem(logoItem) {
      const { name, domain, logo} = logoItem;
      const deleteTarget = {
        name,
        domain,
        logo
      }
    //Send to parent
      this.$emit('delete-item', deleteTarget);
    }
    }
  }
  

</script>

<style scoped>
  li {
    display: flex;
  }


  button {
    width: 20px;
    height: 20px;
    position: relative;
    bottom: 3.65em;
    left: 5.75em;
    background: none;
    border: none;
    font-size: 2em;
    font-weight: bold;
    transform: rotate(45deg);
    cursor: pointer;
    color: #ff4800;
  } 

  span {
    display: block;
    position: relative;
    letter-spacing: .05em;
    font-weight: bold;
  }
 
  .store-container {
    width: 100%;
    height: auto;
    margin: 1em 2em 1em 2em;
    display: flex;
    flex-wrap: wrap;
  }

  .logo-item {
    font-size: .65em;
    background: #c4c4c4;
    width: 140px;
    height: 60px;
    display: inline-block;
    margin: 1em 0 0 1em;
  }

</style>