<template>
  <div id="app">
    <Header @searchedMovie="updateSearch" />
    <Main :series="series" :movies="movies" :inSearching="searched" />
  </div>
</template>

<script>
import Header from "./components/Header";
import Main from "./components/Main";

import axios from "axios";

export default {
  name: "App",
  components: {
    Header,
    Main
  },
  data() {
    return {
      api_url: "https://api.themoviedb.org/3/",
      api_key: "2d86be3565490df0f2e313780db78001",
      lang: "it-IT",
      movies: [],
      series: [],
      searched: false,
    };
  },
  methods: {

    // Assegno la stringa dell'input alla query della chiamata axios ed eseguo la chiamata
    updateSearch(string) {
      if (string == "") {
        return "";
      }
      const params = {
        params: {
          api_key: this.api_key,
          query: string,
          language: this.lang,
        },
      };
      this.getCalls(params)
    },
    getCalls(newParams) {

      // funzione per creare le chiamate axios salvate in costanti 
      const moviesRequest = axios.get(`${this.api_url}search/movie?`, newParams);
      const seriesRequest = axios.get(`${this.api_url}search/tv?`, newParams);

      axios.all([moviesRequest, seriesRequest]).then(
        axios.spread((res1, res2) => {
          this.movies = res1.data.results;
          this.series = res2.data.results;
      
          this.searched = true;
        })
      );
    }
  }
};
</script>

<style lang="scss">
@import "./scss/general";


</style>
