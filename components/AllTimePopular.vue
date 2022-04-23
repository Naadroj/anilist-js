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
import AllTimePopular from "../apollo/queries/AllTimePopular";

export default {
  apollo: {
    Page: {
      query: AllTimePopular,
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
