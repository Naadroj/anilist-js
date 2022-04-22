<template>
  <div>
    <p>
      {{ Media.title.romaji }}
    </p>
  </div>
</template>

<script>
import gql from "graphql-tag";
import OneAnime from "../apollo/queries/OneAnime";

export default {
  apollo: {
    Media: {
      query: OneAnime,
      // variables() {
      //   return {
      //     myVar: this.myVar,
      //   };
      // },
    },
  },
  // data() {
  //   return {
  //     myVar: {
  //       id: 188,
  //     },
  //   };
  // },
};
</script>

<style scoped>
</style>
