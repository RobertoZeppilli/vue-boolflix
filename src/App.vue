<template>
  <div id="app">
    <Header @searchedMovie="updateMovie" />
    <Main :searchedMovie="newMovie" />
  </div>
</template>

<script>
import Header from './components/Header';
import Main from './components/Main';

export default {
  name: 'App',
  components: {
    Header,
    Main
  },
  data() {
    return {
      newMovie: ''
    }
  },
  methods: {
    updateMovie(string) {
      this.newMovie = string
    }
  }
}
</script>

<style lang="scss">
@import './scss/general';

</style>
