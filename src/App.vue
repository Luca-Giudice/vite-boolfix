<script>
import axios from 'axios'
import {api} from './data';
import {store} from './store'
import AppMain from './components/AppMain.vue';
import SearchBar from './components/SearchBar.vue';
import ProductionCard from './components/prodaction/ProductionCard.vue';
export default {
  name: 'Boolflix',
  components: {SearchBar, ProductionCard},
  data: () => ({store, titleFilter: ''}),
  computed: {
    axiosConfig(){
      const {key, language} = api;
      return{
        params: {
          language: language,
          api_key: key,
          query: this.titlefilter
        }
      }
    }
  },
  methods: {
    updateTitleFilter(term){
      this.titleFilter = term
    },
    searchProductions(){
     if(!this.titleFilter) {
      store.movies =[];
      store.series = [];
      return;
     }

     this.fetchApi('search/movie', 'movies');
     this.fetchApi('search/tv', 'series');
     
    },
    fetchApi(endpoint, collection){
      axios.get(`${baseUri}/${endpoint}`, this.axiosConfig).then(res => {
        store[collection] = res.data.results;
      }).catch(err => { console.error(err) });
    }
  }
};
</script>

<template>
  <header>
    <search-bar placeholder="Cerca un film" @term-change="updateTitleFilter" @form-submit="searchProductions"></search-bar>
  </header>
  <app-main></app-main>


</template>

<style></style>
