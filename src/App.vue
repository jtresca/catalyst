<template>
  <div id="app">
    <img id="logo" alt="Logo Lover Logo" src="./assets/images/logolover.png">
    <main class="main-hero-container">
        <div class="right-hero-element">
          <h1 class="callout-text">
            I'm a <br/> <span class="word-highlight">Logo Lover</span>
          </h1>
          <div>
            <LogoSearch v-on:inputChange="apiSearch"/>
            <SuggestResults v-bind:suggest="apiSuggestVals" v-on:add-item="addToCollection"/>
          </div>
        </div>
    </main>
    <section class="bottom-container">
      <p>Hello! I’m Joe Tresca and I love logos. Use the search bar above to add to my collection. I’m always interested in the way the worlds best brands present themselves to their audience. What colors, fonts, type styles and imagery will they use?
         If you have a moment, help me discover the world’s next great logo by using the <span class="word-highlight">+</span> to add it to my collection. Thanks!</p>
      <h3>
      Joe's Collection
    </h3>
    <div class="store">
      <MyLogos v-bind:logoStore="myLogos" v-on:delete-item="deleteFromCollection"/>
    </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios';
import LogoSearch from './components/LogoSearch';
import SuggestResults from './components/SuggestResults';
import MyLogos from './components/MyLogos';

export default {
  name: 'app',
  components: {
    LogoSearch,
    SuggestResults,
    MyLogos
  },
  data() {
    return {
      myLogos: [],
      searchVal: null,
      apiSuggestVals: []
      
    }
  },
  methods:  {
    apiSearch(event) {
      const { value } = event.target;
      this.searchVal = value;
      console.log("HERE IS WHAT I TYPED:", this.searchVal)
      if(this.searchVal ===""){
        this.apiSuggestVals = [];
      }
      else if (this.searchVal) {
        axios.get(`https://autocomplete.clearbit.com/v1/companies/suggest?query=${this.searchVal}`)
        .then(res => {
          //filtering out 
          this.filterMyLogos(res.data);
          this.apiSuggestVals = res.data;
          console.log("SUGGESTED_RESULTS: ", this.apiSuggestVals);
        })
        .catch(err => console.log(err))
      }
    },
    filterMyLogos(apiResponse) {
      console.log("TRIGGERED filteredMyLogos", apiResponse);
    },
    addToCollection(newItem){
      if (this.myLogos.findIndex(x => x.name === newItem.name) < 0) {
        this.myLogos = [...this.myLogos, newItem];
      }
      else { 
       alert("This logo is already in the collection!");
      }
    },
    deleteFromCollection(deleteTarget) {
      const indexOfTarget = this.myLogos.findIndex(i => i.name === deleteTarget.name);
      const lastDeleted = this.myLogos.splice(indexOfTarget, 1);
    }
  }
}
</script>

<style>
 @import './assets/styles/app.css';
</style>
