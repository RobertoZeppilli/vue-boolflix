<template>
  <div class="movie">
      <ul>
          <li>{{ titolo }}</li>
          <li>{{ titoloOriginale }}</li>
          <li>{{ lingua }}</li>
          <li>{{ voto }}</li>
      </ul>
  </div>
</template>

<script>
export default {
    name: 'Movie',
    props: {
        titolo: String,
        titoloOriginale: String,
        lingua: String,
        voto: Number,
    }
}
</script>

<style lang="scss" scoped>

</style>