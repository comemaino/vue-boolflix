<template>
  <div id="app">
    <header>
      <AppHeader
        @searchClicked="
          saveSearchedMovie($event), searchMovie($event), searchTvShows($event)
        "
      />
    </header>
    <main>
      <section class="movies">
        <h2>Movies</h2>
        <div class="container">
          <AppObjCard v-for="item in movies" :key="item.id" :objCard="item" />
        </div>
      </section>
      <section class="series">
        <h2>TV Shows</h2>
        <div class="container">
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
    };
  },

  methods: {
    searchMovie() {
      axios
        .get("https://api.themoviedb.org/3/search/movie", {
          params: {
            api_key: "e5ec05af38ac70f77d47f4a9382f77df",
            query: this.search,
          },
        })
        .then((resp) => {
          this.movies = resp.data.results;
          console.log(this.movies);
        });
    },

    searchTvShows() {
      axios
        .get("https://api.themoviedb.org/3/search/tv", {
          params: {
            api_key: "e5ec05af38ac70f77d47f4a9382f77df",
            query: this.search,
          },
        })
        .then((resp) => {
          this.tvShows = resp.data.results;
          console.log(this.tvShows);
        });
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
</style>
