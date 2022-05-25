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
    </div>
    <div class="details">
      <h4>
        Titolo: <span>{{ cardTitle }}</span>
      </h4>
      <h5>
        Titolo Originale: <span>{{ cardOriginalTitle }}</span>
      </h5>

      <img
        class="flag"
        v-if="this.flags.includes(objCard.original_language)"
        :src="flagImgUrl"
        alt="lang"
      />

      <h6 v-else>{{ objCard.original_language.toUpperCase() }}</h6>

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
      </div>

      <div class="overview">
        <h5 v-if="objCard.overview">
          Overview: <span> {{ objCard.overview }}</span>
        </h5>
      </div>
      <div class="cast">
        <h5>
          Cast:
          <span v-for="(item, index) in this.objCard.cast" :key="index"
            >{{ objCard.cast[index].name }},
          </span>
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
  },
};
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
      margin-bottom: 0.3rem;
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

      .overview {
        max-height: 6rem;
        overflow-y: auto;

        &::-webkit-scrollbar {
          width: 2px;
          height: 100px;
          background-color: #222;
        }
        &::-webkit-scrollbar-thumb {
          background-color: #444;
        }
      }
    }
  }
}
</style>
