<template>
  <div>
    <div class="row" v-if="Page.media">
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
    <div class="actions">
      <button v-if="showMoreEnabled" @click="showMore">Show more</button>
    </div>

    <!-- {{ Page }} -->
  </div>
</template>

<script>
import gql from "graphql-tag";
import AnimeByGenre from "../apollo/queries/AnimeByGenre";

export default {
  data() {
    return {
      Page: {
        media: [],
      },
      page: 0,
      pageSize: 12,
      showMoreEnabled: true,
    };
  },
  props: {
    genre: String,
  },
  apollo: {
    Page: {
      query: AnimeByGenre,
      variables() {
        return {
          genre: this.genre,
          page: this.page,
          perPage: this.pageSize,
        };
      },
    },
  },
  methods: {
    showMore() {
      this.page++;
      console.log(this.page);
      // Fetch more data and transform the original result

      this.$apollo.queries.Page.fetchMore({
        // New variables
        variables: {
          page: this.page,
        },
        // Transform the previous result with new data
        updateQuery: (previousResult, { fetchMoreResult }) => {
          const newMedias = fetchMoreResult.Page.media;
          const newPageInfos = fetchMoreResult.Page.pageInfo;
          const hasMore = fetchMoreResult.Page.hasMore;

          this.showMoreEnabled = hasMore;

          return {
            Page: {
              __typename: previousResult.Page.__typename,
              // Merging the tag list
              media: [...previousResult.Page.media, ...newMedias],
              pageInfo: [...previousResult.Page.pageInfo, ...newPageInfos],
              hasMore,
            },
          };
        },
      });
    },
  },
};
</script>

<style scoped>
</style>
