<template>
  <main class="d-flex flex-wrap" :class="inSearching == true ? 'pt-100' : ''">
    <video
      v-if="!inSearching"
      src="../assets/background-video.mp4"
      muted
      loop
      autoplay
    ></video>
    <Movie
      v-else
      v-for="(item, index) in items"
      :key="index"
      :title="item.title || item.name"
      :originalTitle="item.original_title || item.original_name"
      :language="item.original_language"
      :vote="item.vote_average"
      :poster="item.poster_path"
      :overview="item.overview"
      :backPoster="item.backdrop_path"
      :singleMovie="item"
    />
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
    items: Array,
    inSearching: Boolean,
  },
};
</script>

<style lang="scss" scoped>
@import '../scss/variables';

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