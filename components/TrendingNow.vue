<template>
  <div>
    <h2>TRENDING NOW</h2>
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
        <span class="media-title">
          {{ el.title.romaji }}
        </span>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
import gql from "graphql-tag";
import TrendingNow from "../apollo/queries/TrendingNow";

export default {
  data() {
    return {
      Page: {
        media: [],
      },
      // myVar: {
      //   $perPage: 6,
      // },
      maxElems: 6,
    };
  },
  // mounted() {
  //   console.log(this.pagePage);
  // },
  apollo: {
    Page: {
      query: TrendingNow,
      variables() {
        return {
          myVar: this.myVar,
        };
      },
    },
  },
};
</script>
