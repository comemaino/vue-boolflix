<template>
  <div>
    <input type="text" placeholder="Cerca" v-model="searchedKeys" />
    <button @click="$emit('searchClicked', searchedKeys)">Search</button>
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

<style></style>
