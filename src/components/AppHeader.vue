<template>
  <div class="header">
    <div class="container">
      <h1>BOOLFLIX</h1>
      <input
        type="text"
        placeholder="Cerca"
        v-model="searchedKeys"
        @keyup.enter="$emit('searchClicked', searchedKeys)"
      />
      <!-- <button @click="$emit('searchClicked', searchedKeys)">Search</button> -->
    </div>
    <div class="container">
      <div
        class="genre"
        v-for="(item, index) in genres"
        :key="index"
        @click="$emit('genreClicked', clickedGenre)"
      >
        {{ item.name }}
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "AppHeader",
  props: {
    clickedGenre: Object,
  },
  data() {
    return {
      searchedKeys: "",
      genres: [],
    };
  },

  mounted() {
    axios
      .get(`https://api.themoviedb.org/3/genre/movie/list`, {
        params: {
          api_key: "e5ec05af38ac70f77d47f4a9382f77df",
        },
      })
      .then((resp) => {
        this.genres = resp.data.genres;
        console.log(this.genres);
      });
    // return this.genres;
  },
};
</script>

<style lang="scss" scoped>
@import "../style/common.scss";

.header {
  margin-bottom: 1rem;
  padding: 1rem 0;
  background-color: #111;
  h1 {
    color: #c00;
  }
  input {
    margin: 0.5rem;
  }

  .genre {
    margin: 0.5rem;
    color: #ccc;
    cursor: pointer;
  }
}
</style>
