<template>
  <div class="obj-card">
    <h3>{{ objCard.title ? objCard.title : objCard.name }}</h3>
    <h4>
      {{
        objCard.original_title ? objCard.original_title : objCard.original_name
      }}
    </h4>

    <img v-if="imgUrl" :src="imgUrl" alt="lang" />
    <h5 v-else>{{ objCard.original_language.toUpperCase() }}</h5>

    <h5>{{ objCard.vote_average }}</h5>
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
      imgUrl: require("../assets/img/flags/" +
        this.objCard.original_language +
        ".png"),
    };
  },
};
</script>

<style lang="scss" scoped>
.obj-card {
  width: calc(100% / 4 - 1rem);
  margin: 0.5rem;
  padding: 0.5rem;
  border: 1px solid black;

  img {
    width: 15px;
  }
}
</style>
