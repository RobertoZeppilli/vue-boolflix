<template>
  <header class="d-flex justify-content-between align-items-center px-4">
    <div class="logo">
      <a href="/">
        <img src="../assets/logo-boolflix.png" alt="logo" />
      </a>
    </div>
    <div class="input-bar">
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
    };
  },
};
</script>

<style lang="scss" scoped>
@import '../scss/variables';

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
  .input-bar {
    input {
      border: none;
      border-radius: 5px;
      background-color: transparent;
      border: 1px solid $secondaryText;
      outline: none;
      transition: box-shadow .5s ease-in-out;
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
      transition: transform .5s ease-in-out;
      &:hover {
        transform: scale(1.2);
      }
    }
  }
}
</style>