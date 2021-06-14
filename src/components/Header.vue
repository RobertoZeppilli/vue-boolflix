<template>
  <header class="d-flex justify-content-between align-items-center px-2">
      <div class="logo">
          <a href="#">
              <img src="../assets/logo-boolflix.png" alt="logo">
          </a>
      </div>
      <div class="input-bar">
          <input @keyup="$emit('searchedMovie', movieChoosed)" v-model.trim="movieChoosed" type="text" id="search">
          <button @click="$emit('searchedMovie', movieChoosed)" class="ms-1" for="search">Search</button>
      </div>
  </header>
</template>

<script>
export default {
    name: 'Header',
    data() {
        return {
            movieChoosed: ''
        }
    }
}
</script>

<style lang="scss" scoped>
header {
    height: 100px;
    background-color: grey;
}

button {
    outline: none;
    border: none;
}
</style>