<template>
  <div class="movie">
    <ul>
      <li>{{ titolo }}</li>
      <li>{{ titoloOriginale }}</li>
      <li>
        <img v-if="lingua == 'it'" src="../assets/it.png" alt="language" />
        <img v-else-if="lingua == 'en'" src="../assets/en.png" alt="language">
      </li>
      <li>{{ voto }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Movie",
  props: {
    titolo: String,
    titoloOriginale: String,
    lingua: String,
    voto: Number,
  }
};
</script>

<style lang="scss" scoped>
@import "../scss/general";
.movie {
  background-color: yellow;
  width: calc(100% / 4 - 2rem);
  margin: 1rem;
}

img {
    width: 30px;
}
</style>