<script>
import axios from 'axios'
import {api} from './data';
import {store} from './store'
import SearchBar from './components/SearchBar.vue';
export default {
  name: 'Boolflix',
  components: {SearchBar},
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
  };
  methods: {
    umdateTitleFilter(term){
      this.titleFilter = term
    },
    searchMovies(){
     if(!titleFilter) {
      this.movies =[];
      return;
     }
      const { key, baseUri, language} = api;
      axios.get(`${baseUri}/search/movie`, this.axiosConfig).then(res => {
        store.movies = res.data.results
      }).catch(err => {console.error(err)});
    }
  }
};
</script>

<template>
  <header>
    <search-bar placeholder="Cerca un film" @term-change="updateTitleFilter"></search-bar>
  </header>
  <main>
    <section>
      <h2>
        Movies
      </h2>
      <ul v-for="movie in store.movies" :key="movie.id">
        <li>
          {{movie.title}}
        </li>
        <li>
          {{ movie.original_title }}
        </li>
        <li>
          {{ movie.original_language }}
        </li>
        <li>
          {{ movie.vote_avarage }}
        </li>
      </ul>
    </section>
  </main>


</template>

<style></style>
