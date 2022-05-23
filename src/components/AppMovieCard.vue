<template>
  <div class="movie-card">
    <h3>{{ movie.title }}</h3>
    <h4>{{ movie.original_title }}</h4>
    <h5>{{ movie.original_language }}</h5>
    <h5>{{ movie.vote_average }}</h5>
  </div>
</template>

<script>
export default {
  name: "AppMovieCard",
  props: {
    movie: Object,
  },
};
</script>

<style lang="scss" scoped>
.movie-card {
  margin: 1rem;
  padding: 0.5rem;
  border: 1px solid black;
}
</style>
