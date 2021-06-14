<template>
  <div id="app">
    <Header @searchedMovie="updateSearch" />
    <main class="d-flex flex-wrap">
      <Movie
        v-for="(movie, index) in movies"
        :key="index"
        :titolo="movie.title"
        :titoloOriginale="movie.original_title"
        :lingua="movie.original_language"
        :voto="movie.vote_average"
      />
    </main>
  </div>
</template>

<script>
import Header from "./components/Header";
import Movie from "./components/Movie";

import axios from "axios";

export default {
  name: "App",
  components: {
    Header,
    Movie,
  },
  data() {
    return {
      api_url: "https://api.themoviedb.org/3/search/movie?",
      api_key: "api_key=2d86be3565490df0f2e313780db78001",
      query: "",
      movies: []
    };
  },
  methods: {
    updateSearch(string) {
      this.query = string;
      axios
        .get(`${this.api_url}${this.api_key}&query=${this.query}`)
        .then((res) => {
          this.movies = res.data.results;
          console.log(this.movies);
        });
    },
  }
};
</script>

<style lang="scss">
@import "./scss/general";
</style>
