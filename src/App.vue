<template>
  <div id="app">
    <header>
      <AppHeader
        @searchClicked="saveSearchedMovie($event), searchMovie($event)"
      />
    </header>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    AppHeader,
  },

  data() {
    return {
      movies: [],
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
          this.movies = resp.data;
          console.log(this.movies);
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
</style>
