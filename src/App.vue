<template>
  <div id="app">
    <Header @searchedMovie="updateSearch" />
    <main class="d-flex flex-wrap">
      <video
        v-if="!searched"
        src="./assets/background-video.mp4"
        muted
        loop
        autoplay
      ></video>
      <Movie
        v-else
        v-for="(movie, index) in moviesAndSeries"
        :key="index"
        :titolo="movie.title || movie.name"
        :titoloOriginale="movie.original_title || movie.original_name"
        :lingua="movie.original_language"
        :voto="movie.vote_average"
        :poster="movie.poster_path"
        :trama="movie.overview"
        :backPoster="movie.backdrop_path"
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
      api_movie: "https://api.themoviedb.org/3/search/movie?",
      api_series: "https://api.themoviedb.org/3/search/tv?",
      api_key: "api_key=2d86be3565490df0f2e313780db78001",
      query: "",
      movies: [],
      series: [],
      searched: false,
    };
  },
  methods: {
    updateSearch(string) {
      this.query = string;
      const moviesRequest = axios.get(
        `${this.api_movie}${this.api_key}&query=${this.query}`
      );
      const seriesRequest = axios.get(
        `${this.api_series}${this.api_key}&query=${this.query}`
      );
      axios.all([moviesRequest, seriesRequest]).then(
        axios.spread((res1, res2) => {
          this.movies = res1.data.results;
          this.series = res2.data.results;
          console.log(this.movies)
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
main {
  padding-top: 100px;
  height: 100vh;
  position: relative;
  z-index: 1;
  background-color: $primaryBg;
  video {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}
</style>
