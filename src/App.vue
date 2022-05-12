<template>
  <div id="App">
    <header>
      <h1 class="text-center display-6">Prova</h1>
      <search-bar @performSearch="search" :loader="loading"/>
    </header>
    <main>
      <app-grid :items="movies" title="Movies" :loader="loading"/>
      <app-grid :items="series" title="Series" :loader="loadingSeries"/>
    </main>
   
  </div>
</template>

<script>
import AppGrid from './components/AppGrid.vue'
import SearchBar from './components/SearchBar.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    SearchBar,
    AppGrid
  },
  data(){
    return{
      apiKey: '1db971936b4a663499a5805602ee380c',
      apiPath: 'https://api.themoviedb.org/3/search/',
      movies:[],
      series:[],
      loading: false,
      loadingSeries: false,
    }
  },
  methods:{
    getMovies(queryParams){
      axios.get(this.apiPath+'movie', queryParams).then((res)=>{
        //console.log(res.data.results)
        this.movies = res.data.results;
        this.loading = false;
      }).catch((error)=>{
        console.log(error);
      })
    },
    getSeries(queryParams){
      axios.get(this.apiPath+'tv', queryParams).then((res)=>{
        //console.log(res.data.results)
        this.series = res.data.results;
        this.loadingSeries = false;
      }).catch((error)=>{
        console.log(error);
      })
    },
    search(text){
      //console.log(text);
      const queryParams = {
        params:{
          api_key: this.apiKey,
          query: text
        }
      }
      this.loading = true;
      this.loadingSeries = true;
      this.getMovies(queryParams)
      this.getSeries(queryParams)
    }
  }
  //results
  //id
  //title
  //original_language
  //vote_average
}
</script>

<style lang="scss">
  @import './styles/generals.scss';
 
</style>
