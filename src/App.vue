<template>
  <div id="app">
    <header>
      <AppHeader
        @searchClicked="saveSearchedMovie($event), searchMovie($event)"
      />
    </header>
    <main>
      <section class="movies">
        <div class="container">
          <h2 v-if="this.movies.length != 0">Movies</h2>

          <AppObjCard v-for="item in movies" :key="item.id" :objCard="item" />
        </div>
      </section>
      <section class="series">
        <div class="container">
          <h2 v-if="this.tvShows.length != 0">TV Shows</h2>
          <AppObjCard v-for="item in tvShows" :key="item.id" :objCard="item" />
        </div>
      </section>
    </main>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AppObjCard from "./components/AppObjCard.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    AppHeader,
    AppObjCard,
  },

  data() {
    return {
      movies: [],
      tvShows: [],
      search: "",
      convertedVote: "",
    };
  },

  methods: {
    searchMovie() {
      const options = {
        params: {
          api_key: "e5ec05af38ac70f77d47f4a9382f77df",
          query: this.search,
        },
      };
      //SINTASSI CHIAMATE MULTIPLE
      const reqMovies = axios.get(
        "https://api.themoviedb.org/3/search/movie",
        options
      );
      const reqTvs = axios.get(
        "https://api.themoviedb.org/3/search/tv",
        options
      );

      axios.all([reqMovies, reqTvs]).then((resp) => {
        this.movies = resp[0].data.results;
        console.log(this.movies);
        this.tvShows = resp[1].data.results;
        console.log(this.tvShows);
      });

      // SINTASSI CHAIMATE SEPARATE
      //   axios
      //     .get("https://api.themoviedb.org/3/search/movie", options)
      //     .then((resp) => {
      //       this.movies = resp.data.results;
      //       console.log(this.movies);
      //     });

      //   axios
      //     .get("https://api.themoviedb.org/3/search/tv", options)
      //     .then((resp) => {
      //       this.tvShows = resp.data.results;
      //       console.log(this.tvShows);
      //     });
    },

    saveSearchedMovie(searchedMovie) {
      this.search = searchedMovie;
      console.log(this.search);
    },
  },
};
</script>

<style lang="scss">
@import "~@fortawesome/fontawesome-free/css/all.min.css";
@import "./style/common.scss";

#app {
  height: 100vh;
  background-color: #333;

  main {
    background-color: inherit;

    section {
      h2 {
        margin-bottom: 1rem;
        width: 100%;
        color: #ccc;
      }
    }
  }
}
</style>
