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
  </div>
</template>

<script>
export default {
  name: "AppHeader",
  data() {
    return {
      searchedKeys: "",
    };
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
}
</style>
