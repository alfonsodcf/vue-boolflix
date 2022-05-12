<template>
  <div id="App">
    <header>
      <h1 class="text-center display-6">Prova</h1>
      <search-bar @performSearch="search"/>
    </header>
    <main>
      
      <ul>
        <li v-for="(movie) in movies" :key="movie.id">
          id: {{movie.id}}
          titolo originale: {{movie.original_titolo}}
          titolo: {{movie.title}}
          lingua: {{movie.original_language}}
          voto: {{movie.vote_average}} 
  
        </li>
      </ul>
      <app-grid/>
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
      movies:[]
    }
  },
  methods:{
    getMovies(queryParams){
      axios.get(this.apiPath+'movie', queryParams).then((res)=>{
        //console.log(res.data.results)
        this.movies = res.data.results;
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
      this.getMovies(queryParams)
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
