<template>
  <div>
    <ul>
      <li v-for="el in Page.media" :key="el.id">
        {{ el.title.romaji }}
      </li>
    </ul>
  </div>
</template>

<script>
import gql from "graphql-tag";
import Top100Anime from "../apollo/queries/Top100Anime";

export default {
  apollo: {
    Page: {
      query: Top100Anime,
      variables() {
        return {
          myVar: this.myVar,
        };
      },
    },
  },
};
</script>

<style scoped>
</style>
