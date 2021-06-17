<template>
  <header class="d-flex justify-content-between align-items-center px-4">
    <div class="logo">
      <a href="/">
        <img src="../assets/logo-boolflix.png" alt="logo" />
      </a>
    </div>
    <div class="search d-flex align-items-center">
      <div class="selects" v-if="inSearching">
        <select
          v-model="choosedMovieGenre"
          @change="$emit('updateMovieGenre', choosedMovieGenre.toString())"
        >
          <option value="">Filtra Film</option>
          <option
            v-for="(movieName, index) in movieNames"
            :key="index"
            :value="movieName.id"
          >
            {{ movieName.name }}
          </option>
        </select>
        <select
          v-model="choosedSerieGenre"
          @change="$emit('updateSerieGenre', choosedSerieGenre.toString())"
        >
          <option value="">Filtra Serie</option>
          <option
            v-for="(serieName, index) in serieNames"
            :key="index"
            :value="serieName.id"
          >
            {{ serieName.name }}
          </option>
        </select>
      </div>
      <input
        class="p-1 px-2"
        @keyup.enter="$emit('searchedMovie', movieChoosed)"
        v-model.trim="movieChoosed"
        type="text"
        placeholder="Cerca un film o una serie..."
      />
      <i
        @click="$emit('searchedMovie', movieChoosed)"
        class="fas fa-search ms-4"
      ></i>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      movieChoosed: "",
      choosedMovieGenre: "",
      choosedSerieGenre: "",
    };
  },
  props: {
    movieNames: Array,
    serieNames: Array,
    inSearching: Boolean
  }
};
</script>

<style lang="scss" scoped>
@import "../scss/variables";

header {
  height: 100px;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.4);
  position: fixed;
  top: 0;
  z-index: 2;
  img {
    height: 80px;
  }
  .search {
    input {
      border: none;
      border-radius: 5px;
      background-color: transparent;
      border: 1px solid $secondaryText;
      outline: none;
      transition: box-shadow 0.5s ease-in-out;
      width: 300px;
      color: $primaryText;
      &:hover {
        box-shadow: 3px 3px 3px red;
      }
      &::placeholder {
        color: $primaryText;
      }
    }
    i {
      font-size: 25px;
      color: $secondaryText;
      cursor: pointer;
      transition: transform 0.5s ease-in-out;
      &:hover {
        transform: scale(1.2);
      }
    }
  }
}
select {
  padding: 0.28rem;
  margin-right: 20px;
  background: transparent;
  border: 1px solid $secondaryText;
  border-radius: 5px;
  color: $secondaryText;
  transition: box-shadow 0.5s ease-in-out;
  &:hover {
    box-shadow: 3px 3px 3px red;
  }
}
</style>