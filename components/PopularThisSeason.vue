<template>
  <div>
    <h2>POPULAR THIS SEASON</h2>
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
          <span v-if="el.title.romaji.length <= 35" class="media-title">
            {{ el.title.romaji }}
          </span>
          <span v-else class="media-title">
            {{ el.title.romaji.slice(0, 35) + "..." }}
          </span>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
import PopularThisSeason from "../apollo/queries/PopularThisSeason";

export default {
  data() {
    return {
      Page: {
        media: [],
      },
      MediaSeason: {
        WINTER: "WINTER",
        SPRING: "SPRING",
        SUMMER: "SUMMER",
        FALL: "FALL",
      },
      maxElems: 6,
    };
  },
  apollo: {
    Page: {
      query: PopularThisSeason,
        // TODO: don't hard set season
      variables() {
        return {
          year: new Date().getFullYear(),
        };
      },
    },
  },
};
</script>

<style scoped>
</style>
