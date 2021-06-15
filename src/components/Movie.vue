<template>
  <section class="movie">
    <div class="poster d-flex">
      <img :src="getImg" :alt="titolo" v-if="poster" />
      <img v-else src="../assets/substitute.jpg" :alt="titolo" />
      <div class="info text-center overflow">
        <div class="info-container p-3">
          <h5>
            Titolo: 
            <span>{{ titolo }}</span>
          </h5>
          <h5>
            Titolo Originale: 
            <span>{{ titoloOriginale }}</span>
          </h5>
          <span v-if="trama.length > 0">Trama:
            <p>{{ trama }}</p>
          </span>
          <div class="lang d-flex align-items-center mb-3">
            <span class="me-2">Lingua: </span>
            <img v-if="lingua == 'it'" src="../assets/it.png" alt="language" />
            <img
              v-else-if="lingua == 'en'"
              src="../assets/en.png"
              alt="language"/>
            <span class="grey" v-else>{{ lingua }}</span>
          </div>
          <div class="vote d-flex align-items-center">
            <span
              >Voto:
              <i
                class="me-1"
                v-for="i in 5"
                :key="i"
                :class="i <= roundVote ? 'fas fa-star' : 'far fa-star'"
              ></i>
            </span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "Movie",
  props: {
    titolo: String,
    titoloOriginale: String,
    lingua: String,
    poster: String,
    voto: Number,
    trama: String,
    backPoster: String,
  },
  data() {
    return {
      img: "https://image.tmdb.org/t/p/w342",
    };
  },
  computed: {
    getImg() {
      return `${this.img}${this.poster}`;
    },
    roundVote() {
      return Math.round(this.voto / 2);
    }
  },
};
</script>

<style lang="scss" scoped>
@import "../scss/general";
.movie {
  width: calc(100% / 4);
  height: auto;
}
.poster {
  position: relative;
  width: 100%;
  height: 100%;
  img {
    width: 100%;
    object-fit: cover;
    object-position: center;
  }
}

.info {
  display: none;
  position: absolute;
  width: 100%;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.8);
  color: #fff;

  p {
    font-size: 0.63em;
    color: $primaryText;
  }
}
.info-container {
  width: 100%;
  text-align: left;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.poster:hover .info {
  display: block;
}
.lang {
  width: 100%;
  text-align: left;
}
.lang img {
  width: 40px;
}

h5 {
  font-size: 1em;
  color: $secondaryText;
  span {
    color: $primaryText;
  }
}
.grey {
  color: $primaryText;
}

.vote {
  i {
    color: hsla(61, 96%, 51%, 0.781);
  }
}
</style>