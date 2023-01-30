<script>
import axios from 'axios'
import {api} from './data';
import {store} from './store'
import SearchBar from './components/SearchBar.vue';
export default {
  name: 'Boolflix',
  components: {SearchBar},
  data: () => ({store, titleFilter: ''}),
  methods: {
    umdateTitleFilter(term){
      this.titleFilter = term
    },
    searchMovies(){
      //
      axios.get()
    }
  }
};
</script>

<template>
  <header>
    <search-bar placeholder="Cerca un film" @term-change="updateTitleFilter"></search-bar>
  </header>


</template>

<style></style>
