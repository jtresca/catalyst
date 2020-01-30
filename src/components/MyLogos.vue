<template>
  <div class="store-container">
    <ul  v-bind:key="logo.id" v-for="logo in logoStore">
      <li class="logo-item"><img :src="logo.logo" height="60" width="60"><span>{{logo.name}}</span><button>+</button></li> 
    </ul>
  </div>
</template>

<script>
export default {
  name: "MyLogos",
  props: ["logoStore"],
  methods: {
    addItem() {
      
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
    bottom: 3.25em;
    left: 5em;
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
    font-size: .75em;
    background: #c4c4c4;
    width: 140px;
    height: 60px;
    display: inline-block;
    margin: 1em 0 0 1em;
  }

</style>