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
    <section>
      <h2>
        Series
      </h2>
      <ul v-for="serie in store.series" :key="serie.id">
        <li>
          {{serie.name}}
        </li>
        <li>
          {{ serie.original_name}}
        </li>
        <li>
          {{ serie.original_language }}
        </li>
        <li>
          {{ serie.vote_avarage }}
        </li>
      </ul>
    </section>
  </main>


</template>

<style></style>
