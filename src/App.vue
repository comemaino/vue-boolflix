<template>
  <div id="app">
    <header>
      <AppHeader
        @searchClicked="saveSearchedMovie($event), searchMovie($event)"
        @genreClicked="filterGenres($event)"
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
      movieCast: [],
      search: "",
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
        const movies = resp[0].data.results;
        const tvShows = resp[1].data.results;

        movies.forEach((element) => {
          axios
            .get(`https://api.themoviedb.org/3/movie/${element.id}/credits`, {
              params: {
                api_key: "e5ec05af38ac70f77d47f4a9382f77df",
              },
            })
            .then((resp) => {
              // console.log(resp);
              element.cast = resp.data.cast.splice(0, 5);
              this.movies.push(element);
            });
        });

        tvShows.forEach((element) => {
          axios
            .get(`https://api.themoviedb.org/3/tv/${element.id}/credits`, {
              params: {
                api_key: "e5ec05af38ac70f77d47f4a9382f77df",
              },
            })
            .then((resp) => {
              // console.log(resp);
              element.cast = resp.data.cast.splice(0, 5);
              this.tvShows.push(element);
            });
        });
      });
    },

    filterGenres() {},

    saveSearchedMovie(searchedMovie) {
      this.search = searchedMovie;
      console.log(this.search);
    },
  },

  // computed: {
  //   castMembers,
  // },
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
