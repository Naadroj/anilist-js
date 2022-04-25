<template>
  <div>
    <div class="row">
      <div
        class="col-12 col-sm-6 col-md-4 col-xl-2"
        v-for="el in Page.media"
        :key="el.id"
      >
        <b-card
          :img-src="el.coverImage.extraLarge"
          :img-alt="el.title.romaji"
          class="mb-2"
        >
        </b-card>
        <span class="media-title">
          {{ el.title.romaji }}
        </span>
      </div>
    </div>
    <!-- {{ Page }} -->
  </div>
</template>

<script>
import gql from "graphql-tag";
import AnimeByGenre from "../apollo/queries/AnimeByGenre";

export default {
  props: {
    genre: String,
  },
  apollo: {
    Page: {
      query: AnimeByGenre,
      variables() {
        return {
          genre: this.genre,
          perPage: 20,
        };
      },
    },
  },
  data() {
    return {
      Page: {
        media: [],
      },
    };
  },
  methods: {
    typeOfVar: function (variable) {
      return Object.prototype.toString.apply(variable);
    },
  },
};
</script>

<style scoped>
</style>
