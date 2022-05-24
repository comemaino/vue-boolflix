<template>
  <div class="header">
    <div class="container">
      <input type="text" placeholder="Cerca" v-model="searchedKeys" />
      <button @click="$emit('searchClicked', searchedKeys)">Search</button>
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
  background-color: #555;
  padding: 1rem 0;
}
</style>
