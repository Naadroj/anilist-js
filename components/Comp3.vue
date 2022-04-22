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
import SomeAnimes from "../apollo/queries/SomeAnimes";

export default {
  apollo: {
    Page: {
      query: SomeAnimes,
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
