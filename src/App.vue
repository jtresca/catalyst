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
      <p>Hello! I’m Joe Tresca and I love logos. Use the search bar above to add to my collection. I’m always interested in the way the world's best brands present themselves to their audience. What colors, fonts, type styles and imagery will they use?
         If you have a moment, you can suggest that I look at a logo you think is awesome by using the <span class="word-highlight">+</span> to add it to my collection. Thanks!</p>
      <h3>
      Joe's Collection: <div class="logo-count">{{myLogos.length}}</div>
    </h3>
    <p v-if="this.myLogos.length <= 0">Joe's Collection is empty right now.</p>
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
      if(this.searchVal ===""){
        this.apiSuggestVals = [];
      }
      else if (this.searchVal) {
        this.getApiData();
      }
    },
    getApiData(){
      axios.get(`https://autocomplete.clearbit.com/v1/companies/suggest?query=${this.searchVal}`)
        .then(res => {
          //filtering out the logos we already have in our collection from suggested results.
          this.apiSuggestVals =  this.filterMyLogos(res.data);
          console.log("SUGGESTED_RESULTS: ", this.apiSuggestVals);
        })
        .catch(err => console.log(err))
    },
    filterMyLogos(apiResponse) {
      return apiResponse = apiResponse.filter(ar => !this.myLogos.find(rm => (rm.name === ar.name) ))
    },
    addToCollection(newItem){
      if (this.myLogos.findIndex(x => x.name === newItem.name) < 0) {
        this.myLogos = [...this.myLogos, newItem];
        this.getApiData();
      }
      else { 
       alert("This logo is already in the collection!");
      }
    },
    deleteFromCollection(deleteTarget) {
      const indexOfTarget = this.myLogos.findIndex(i => i.name === deleteTarget.name);
      this.myLogos.splice(indexOfTarget, 1);
      this.getApiData();
    }
  }
}
</script>

<style>
 @import './assets/styles/app.css';
</style>
