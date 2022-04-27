<template>
  <div>
    <h2>ALL TIME POPULAR</h2>
    <div class="row">
      <div
        class="col-12 col-sm-6 col-md-4 col-xl-2"
        v-for="el in Page.media.slice(0, maxElems)"
        :key="el.id"
      >
      <NuxtLink :to="el.id.toString()">
        <b-card
          :img-src="el.coverImage.extraLarge"
          :img-alt="el.title.romaji"
          class="mb-2"
        >
        </b-card>
        <span  v-if="el.title.romaji.length <= 35" class="media-title">
          {{ el.title.romaji }}
        </span>
        <span v-else class="media-title">
          {{ el.title.romaji.slice(0, 35) + '...' }}
        </span>
      </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
import gql from "graphql-tag";
import AllTimePopular from "../apollo/queries/AllTimePopular";

export default {
  data() {
    return {
      Page: {
        media: [],
      },
      // MediaSeason: {
      //   WINTER: "WINTER",
      //   SPRING: "SPRING",
      //   SUMMER: "SUMMER",
      //   FALL: "FALL",
      // },
      // season: this.MediaSeason.winter,
      maxElems: 6,
    };
  },
  // TODO: don't hard set year and season
  apollo: {
    Page: {
      query: AllTimePopular,
      variables: {
        // season: this.MediaSeason,
        // year: 2022,
        // myVar: this.myVar,
      },
    },
  },
};
</script>

<style scoped>
</style>
