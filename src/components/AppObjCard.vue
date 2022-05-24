<template>
  <div class="obj-card">
    <div class="cover">
      <img
        :src="posterImgUrl"
        :alt="objCard.title ? objCard.title : objCard.name"
      />

      <!-- {{ objCard.poster_path }} -->
    </div>
    <div class="hover">
      <h3>{{ objCard.title ? objCard.title : objCard.name }}</h3>
      <h4>
        {{
          objCard.original_title
            ? objCard.original_title
            : objCard.original_name
        }}
      </h4>

      <!-- <img
        v-if="flagImgUrl"
        :src="
          require('../assets/img/flags/' +
            this.objCard.original_language +
            '.png')
        "
        alt="lang"
        class="flag"
      />
      <h5 v-else>{{ objCard.original_language.toUpperCase() }}</h5> -->

      <img
        class="flag"
        v-if="this.flags.includes(objCard.original_language)"
        :src="flagImgUrl"
        alt="lang"
      />

      <h5 v-else>{{ objCard.original_language.toUpperCase() }}</h5>

      <h5>{{ convertedRate }}</h5>

      <div class="rating-container">
        <i
          class="fas fa-star"
          v-for="(item, index) in this.fullStars"
          :key="index"
          :fullStar="item"
        ></i>
        <i
          class="far fa-star"
          v-for="(item, index) in this.emptyStars"
          :key="index"
          :emptyStar="item"
        ></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppObjCard",
  props: {
    objCard: Object,
  },

  data() {
    return {
      flags: ["de", "en", "fr", "it", "ja", "jp"],
    };
  },

  computed: {
    flagImgUrl() {
      return require("../assets/img/flags/" +
        this.objCard.original_language +
        ".png");
    },

    posterImgUrl() {
      return "https://image.tmdb.org/t/p/w154" + this.objCard.poster_path;
    },

    convertedRate() {
      return Math.ceil(this.objCard.vote_average / 2);
    },

    fullStars() {
      const fullStarsArray = [];
      for (let i = 0; i < this.convertedRate; i++) {
        fullStarsArray.push(i);
      }
      return fullStarsArray;
    },

    emptyStars() {
      const empties = 5 - this.convertedRate;
      const emptyStarsArray = [];
      for (let i = 0; i < empties; i++) {
        emptyStarsArray.push(i);
      }
      return emptyStarsArray;
    },
  },
};
// console.log(stars());
</script>

<style lang="scss" scoped>
.obj-card {
  width: calc(100% / 4 - 1rem);
  margin: 0.5rem;
  padding: 0.5rem;
  border: 1px solid black;

  .cover img {
    width: 100%;
  }

  .flag {
    width: 15px;
  }
}
</style>
