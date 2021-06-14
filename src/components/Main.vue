<template>
  <main>
    <Movie
      v-for="(movie, index) in movies"
      :key="index"
      :titolo="movie.title"
      :titoloOriginale="movie.original_title"
      :lingua="movie.original_language"
      :voto="movie.vote_average"
    />
  </main>
</template>

<script>
import axios from "axios";

import Movie from "./Movie";

export default {
  name: "Main",
  data() {
    return {
      api_key: "api_key=2d86be3565490df0f2e313780db78001",
      api_url: "https://api.themoviedb.org/3/search/movie?",
      query: 'ritorno al futuro',
      movies: [],
    };
  },
  components: {
    Movie,
  },
  props: {
      searchedMovie: String
  },
  created() {
    axios.get(`${this.api_url}${this.api_key}&query=${this.query}`).then((res) => {
      
      this.movies = res.data.results;
      console.log(this.movies);
    });
  },
};
</script>

<style lang="scss" scoped>
</style>