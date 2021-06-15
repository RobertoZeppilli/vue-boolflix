<template>
  <header class="d-flex justify-content-between align-items-center px-2">
    <div class="logo">
      <a href="#">
        <img src="../assets/logo-boolflix.png" alt="logo" />
      </a>
    </div>
    <div class="input-bar">
      <input
        class="p-1 px-2"
        v-model.trim="movieChoosed"
        type="text"
        id="search"
      />
      <button
        @click="$emit('searchedMovie', movieChoosed)"
        class="ms-1 px-3 p-1"
        for="search"
      >
        Search
      </button>
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
header {
  height: 100px;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  position: fixed;
  top: 0;
  z-index: 2;
  img {
    height: 60px;
  }
  button,
  input {
    outline: red;
    border: none;
    border-radius: 5px;
  }
}
</style>