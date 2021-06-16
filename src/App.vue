<template>
  <div id="app">
    <Header @searchedMovie="updateSearch" />
    <Main :items="moviesAndSeries" :inSearching="searched" />
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
      api_movie: "https://api.themoviedb.org/3/search/movie?",
      api_series: "https://api.themoviedb.org/3/search/tv?",
      api_key: "2d86be3565490df0f2e313780db78001",
      lang: "it-IT",
      movies: [],
      series: [],
      searched: false,
    };
  },
  methods: {
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
      const moviesRequest = axios.get(this.api_movie, params);
      const seriesRequest = axios.get(this.api_series, params);

      axios.all([moviesRequest, seriesRequest]).then(
        axios.spread((res1, res2) => {
          this.movies = res1.data.results;
          this.series = res2.data.results;
          console.log(this.movies);
          console.log(this.series);
          this.searched = true;
        })
      );
    },
  },
  computed: {
    moviesAndSeries() {
      return [...this.movies, ...this.series];
    },
  },
};
</script>

<style lang="scss">
@import "./scss/general";


</style>
