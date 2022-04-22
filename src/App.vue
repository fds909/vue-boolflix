<template>
  <div>
    <HeaderComp @search="searchTitle"/>
    <MainComp :films="movies"/>
  </div>
</template>

<script>
import HeaderComp from './components/HeaderComp.vue';
import MainComp from './components/MainComp.vue'
import axios from 'axios';

export default {
  name: 'App',
  components: {
    HeaderComp,
    MainComp
  },
  data() {
    return {
      apiKey: '480ca1b608920c32ceb1d868578f7cdf',
      searchText: '',
      movies: [],
      series: []
    }
  },
  methods: {
    searchTitle(text) {
      this.searchText = text;
      console.log(this.searchText);

      if (this.searchText != '') {
        axios.get( `https://api.themoviedb.org/3/search/movie?api_key=${this.apiKey}&query=${this.searchText}&language=it-IT`)
        .then( (res) => {
          console.log(res.data.results);
          
          res.data.results.forEach(element => {
            let movie = {
              'title': element.title,
              'originalTitle': element.original_title,
              'language': element.original_language,
              'vote': element.vote_average
            }

            this.movies.push(movie);
          });

          console.log(this.movies);
        });
      }
      
    }
  } 
}
</script>

<style lang="scss">
  // Reset
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
</style>
