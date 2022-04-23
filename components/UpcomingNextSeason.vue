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
import UpcomingNextSeason from "../apollo/queries/UpcomingNextSeason";

export default {
  data() {
    return {
      myVar: {
        year: 2022,
        season: "WINTER",
      },
    };
  },
  apollo: {
    Page: {
      query: UpcomingNextSeason,
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
