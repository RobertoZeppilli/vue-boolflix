<template>
  <div id="app">
    <Header @searchedMovie="updateSearch" />
    <main class="d-flex flex-wrap" :class="searched == true ? 'pt-100' : ''">
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
        :title="movie.title || movie.name"
        :originalTitle="movie.original_title || movie.original_name"
        :language="movie.original_language"
        :vote="movie.vote_average"
        :poster="movie.poster_path"
        :overview="movie.overview"
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
      api_key: "2d86be3565490df0f2e313780db78001",
      lang: "it_IT",
      movies: [],
      series: [],
      searched: false,
    };
  },
  methods: {
    updateSearch(string) {
      if(string == '') {
        return ''
      }
      
      const moviesRequest = axios.get(this.api_movie, {
        params: {
          api_key: this.api_key,
          language: this.lang,
          query: string
        }
      });
      const seriesRequest = axios.get(this.api_series, {
        params: {
          api_key: this.api_key,
          language: this.lang,
          query: string
        }
      });
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
main {
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
.pt-100 {
  padding-top: 100px;
}
</style>
