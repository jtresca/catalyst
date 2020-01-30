<template>
  <div class="results">
      <ul v-bind:key="result.id" v-for="result in suggest">
        <li><img :src="result.logo" height="30" width="30"><span>{{result.name}}</span><button @click="addItem(result)">+</button></li>
      </ul>
  </div>
</template>

<script>
export default {
  name: "SuggestResults",
  data() {
    return {
      result: ""
    }
  },
  props: ["suggest"],
  methods: {
    addItem(result) {
      const { name, domain, logo} = result;
      const newItem = {
        name,
        domain,
        logo
      }
      //Send to parent
      this.$emit('add-item', newItem);
      console.log("OBJECT I AM SENDING", newItem);
    }
  }
}
</script>

<style scoped>
  .results {
    margin-top: 1em;
    margin-left:.25em;
  }

  ul {
    padding: 0 .55em 0 .55em;
  }

  li {
    display: flex;
    flex-direction: row;
    text-decoration: none;
    display: block;
    width: 100%;
    height: 30px;
    background: #e4e4e4;
    margin-top: .25em;
    letter-spacing: .05em;
  }

  img {
    margin-bottom: 1px;
    margin-left: -4px;
  }

  span {
    width:75%;
    display: inline-block;
    font-weight: bold;
    position: relative;
    bottom: .75em;
    padding-left: .5em;
    font-size: .75em;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  button {
    font-size: 2em;
    color: #ff4800;
    font-weight: bold;
    font-family: inherit;
    border: 0;
    padding: 0;
    background: none;
    cursor: pointer;
    height: auto;
    position: relative;
    bottom: .22em;
  }
</style>