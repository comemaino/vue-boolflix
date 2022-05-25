<template>
  <div class="obj-card">
    <div class="cover">
      <img
        v-if="this.objCard.poster_path != null"
        :src="posterImgUrl"
        :alt="cardTitle"
      />
      <div v-else class="not-found">
        <img src="../assets/img/not-found.jpg" alt="" />
        <span>{{ cardTitle }}</span>
      </div>
      <!-- {{ objCard.poster_path }} -->
    </div>
    <div class="details">
      <h4>
        Titolo: <span>{{ cardTitle }}</span>
      </h4>
      <h5>
        Titolo Originale: <span>{{ cardOriginalTitle }}</span>
      </h5>

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

      <h6 v-else>{{ objCard.original_language.toUpperCase() }}</h6>

      <!-- <h5>{{ convertedRate }}</h5> -->

      <div class="rating-container">
        <h5>
          Voto:
          <i
            v-for="n in 5"
            :key="n"
            class="fa-star"
            :class="n <= convertedRate ? 'fas' : 'far'"
          ></i>
        </h5>
        <!-- STARS WITH 2 DIFFERENT ARRAYS -->
        <!-- <i
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
        ></i> -->
      </div>

      <div class="overview">
        <h5>
          Overview <span> {{ objCard.overview }}</span>
        </h5>
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
      flags: ["de", "en", "fr", "it", "ja"],
    };
  },

  computed: {
    cardTitle() {
      return this.objCard.title || this.objCard.name;
    },

    cardOriginalTitle() {
      return this.objCard.original_title || this.objCard.original_name;
    },

    flagImgUrl() {
      return require("../assets/img/flags/" +
        this.objCard.original_language +
        ".png");
    },

    posterImgUrl() {
      return "https://image.tmdb.org/t/p/w342" + this.objCard.poster_path;
    },

    convertedRate() {
      return Math.ceil(this.objCard.vote_average / 2);
    },
    // STARS WITH TWO DIFFERENT ARRAYS
    // fullStars() {
    //   const fullStarsArray = [];
    //   for (let i = 0; i < this.convertedRate; i++) {
    //     fullStarsArray.push(i);
    //   }
    //   return fullStarsArray;
    // },

    // emptyStars() {
    //   const empties = 5 - this.convertedRate;
    //   const emptyStarsArray = [];
    //   for (let i = 0; i < empties; i++) {
    //     emptyStarsArray.push(i);
    //   }
    //   return emptyStarsArray;
    // },
  },
};
// console.log(stars());
</script>

<style lang="scss" scoped>
.obj-card {
  margin-bottom: 1rem;
  width: calc(100% / 4 - 1rem);

  .cover {
    img {
      border: 3px solid #ccc;
      width: 100%;
      aspect-ratio: 5 / 8;
    }

    .not-found {
      position: relative;

      span {
        text-align: center;
        width: 100%;
        position: absolute;
        left: 50%;
        top: 1rem;
        transform: translate(-50%, 0);
        color: #fff;
        font-weight: 600;
        text-transform: uppercase;
      }
    }
  }

  .details {
    display: none;

    width: 100%;
    height: 100%;
    background-color: #111;

    * {
      margin-bottom: 0.2rem;
      color: #ccc;
    }
  }
  &:hover {
    .cover {
      display: none;
    }

    .details {
      padding: 0.5rem;

      display: inline-block;

      span {
        font-weight: 400;
      }

      .flag {
        width: 15px;
      }

      i {
        color: #fc0;
      }
    }
  }
}
</style>
