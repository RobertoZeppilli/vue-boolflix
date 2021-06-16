<template>
  <div class="movie">
    <div class="poster d-flex">
      <img :src="getImg" :alt="title" />
      <div class="info text-center">
        <div class="info-container p-3">
          <ul>
            <li><span>Title:</span> {{ title }}</li>
            <li><span>Original Title:</span> {{ originalTitle }}</li>
            <li v-if="overview.length > 0">
              <span>Overview:</span> {{ overview }}
            </li>
            <li class="d-flex">
              <span>Language:</span>
              <img :src="flag" :alt="language" />
            </li>
            <li>
              <span>Vote:</span>
              <i
                class="me-1"
                v-for="i in 5"
                :key="i"
                :class="i <= roundVote ? 'fas fa-star' : 'far fa-star'"
              ></i>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Movie",
  props: {
    title: String,
    originalTitle: String,
    language: String,
    poster: String,
    vote: Number,
    overview: String,
    backPoster: String,
  },
  data() {
    return {
      img: "https://image.tmdb.org/t/p/w342",
      flag: ""
    };
  },
  methods: {
    getFlag() {
      switch (this.language) {
        case "it":
          this.flag = require("../assets/it.png");
          break;
        case "en":
          this.flag = require("../assets/en.png");
          break;
        case "fr":
          this.flag = require("../assets/fr.jpg");
          break;
        case "ja":
          this.flag = require("../assets/ja.png");
          break;
        case "es":
          this.flag = require("../assets/es.png");
          break;
        case "pt":
          this.flag = require("../assets/pt.jpg");
          break;
      }
    },
  },
  computed: {
    getImg() {
      let choosePoster = this.poster;
      if (this.poster != null) {
        return `${this.img}${this.poster}`;
      } else if (this.poster == null) {
        if (this.backPoster != null) {
          return `${this.img}${this.backPoster}`;
        } else {
          return require("../assets/substitute.jpg");
        }
      }
      return choosePoster;
    },
    roundVote() {
      return Math.round(this.vote / 2);
    },
  },
  created() {
    this.getFlag()
  },
};
</script>

<style lang="scss" scoped>
@import "../scss/general";

.movie {
  width: calc(100% / 4);
  height: auto;
  .poster {
    position: relative;
    width: 100%;
    height: 100%;
    &:hover .info {
      display: block;
    }
    img {
      width: 100%;
      object-fit: cover;
      object-position: center;
    }
    .info {
      display: none;
      position: absolute;
      overflow-y: auto;
      width: 100%;
      inset: 0;
      background-color: rgba(0, 0, 0, 0.8);

      .info-container {
        width: 100%;
        text-align: left;
        ul {
          list-style: none;

          & > li {
            padding: 5px 0;
          }
        }
        img {
          width: 30px;
        }
        span {
          margin-right: 5px;
        }
        span:not(.lang) {
          color: $secondaryText;
          font-weight: bold;
        }
        i {
          color: hsla(61, 96%, 51%, 0.781);
        }
      }
    }
  }
}
</style>