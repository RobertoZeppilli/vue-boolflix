<template>
  <main :class="inSearching == true ? 'pt-100 h-auto' : 'vh-100'">
    <div v-if="!inSearching" class="video-container">
      <video src="../assets/background-video.mp4" muted loop autoplay></video>
    </div>
    <div v-else>
      <div v-if="movies.length > 0 || series.length > 0">
        <section
          class="movies"
          v-if="filterMovie.length > 0"
          :class="filterMovie.length == 0 ? 'ciao' : ''"
        >
          <h3 v-if="movies.length > 0">Film</h3>
          <div class="d-flex flex-wrap">
            <Movie
              v-for="(movie, index) in filterMovie"
              :key="index"
              :title="movie.title"
              :originalTitle="movie.original_title"
              :language="movie.original_language"
              :vote="movie.vote_average"
              :poster="movie.poster_path"
              :overview="movie.overview"
              :backPoster="movie.backdrop_path"
              :singleMovie="movie"
            />
          </div>
        </section>
        <section class="series" v-if="filterSerie.length > 0">
          <h3 v-if="series.length > 0">Serie</h3>
          <div class="d-flex flex-wrap">
            <Movie
              v-for="(serie, index) in filterSerie"
              :key="index"
              :title="serie.name"
              :originalTitle="serie.original_name"
              :language="serie.original_language"
              :vote="serie.vote_average"
              :poster="serie.poster_path"
              :overview="serie.overview"
              :backPoster="serie.backdrop_path"
              :singleMovie="serie"
            />
          </div>
        </section>
      </div>
      <div class="no-results" v-else>
        <h3>La ricerca non ha prodotto risultati</h3>
      </div>
    </div>
  </main>
</template>

<script>
import Movie from "../components/Movie";
export default {
  name: "Main",
  components: {
    Movie,
  },
  props: {
    movies: Array,
    series: Array,
    inSearching: Boolean,
    newGenreForMovie: String,
    newGenreForSerie: String,
  },
  computed: {
    filterMovie() {
      if (this.newGenreForMovie == "") {
        return this.movies;
      } else {
        const newArray = this.movies.filter((el) => {
          return el.genre_ids == this.newGenreForMovie;
        });
        return newArray;
      }
    },
    filterSerie() {
      if (this.newGenreForSerie == "") {
        return this.series;
      } else {
        const newArray = this.series.filter((el) => {
          return el.genre_ids == this.newGenreForSerie;
        });
        return newArray;
      }
    }
  },
};
</script>

<style lang="scss" scoped>
@import "../scss/variables";

main {
  position: relative;
  z-index: 1;
  background: $primaryBg;

  .video-container {
    height: 100%;
    overflow: hidden;
    video {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }
  .series,
  .movies {
    margin-top: 30px;
    h3 {
      color: $secondaryText;
      font-weight: bold;
      font-size: 1.8rem;
      text-transform: uppercase;
      letter-spacing: 10px;
      margin: 0 1rem;
    }
  }
}

.pt-100 {
  padding-top: 100px;
}
.no-results {
  height: 85.5vh;
  overflow: hidden;
  color: $secondaryText;
  display: flex;
  justify-content: center;
  align-items: center;
  h3 {
    font-size: 2rem;
    padding: 0 5px;
    position: relative;
    &::after,
    &::before {
      content: "";
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      height: 100%;
    }
    &::before {
      background-color: $primaryBg;
      animation: typeAnimation 2s steps(36) 0.5s forwards;
    }
    &::after {
      width: 0.125em;
      background-color: $secondaryText;
      animation: typeAnimation 2s steps(36) 0.5s forwards,
        cursorEffect 500ms steps(36) infinite;
    }
  }
}
@keyframes scale {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(1.2);
  }
}
@keyframes typeAnimation {
  to {
    left: 100%;
  }
}
@keyframes cursorEffect {
  to {
    background-color: transparent;
  }
}
</style>