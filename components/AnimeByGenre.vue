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
      <button v-if="showMoreEnabled" @click="logger">Show more</button>
    </div>

<!--     {{ Page }} -->
  </div>
</template>

<script>
import gql from "graphql-tag";
import AnimeByGenre from "../apollo/queries/AnimeByGenre";

// ! Need to store fetched datas in an array and push new datas in this array everytime we showMore()
export default {
  data() {
    return {
      Page: {
        media: [],
      },
      page: 0,
      showMoreEnabled: true,
      pageSize : 24,
      toAdd : 24
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
          perPage: 120,
        };
      },
    },
  },
  methods: {
    showMore() {
      // this.page++;
      this.pageSize += this.toAdd
      // Fetch more data and transform the original result

      this.$apollo.queries.Page.fetchMore({
        // New variables
        variables() {
          return {
            // page: this.page,
            perPage: this.pageSize,
          }
        },
        // Transform the previous result with new data
        updateQuery: (previousResult, { fetchMoreResult }) => {
          const newMedias = fetchMoreResult.Page.media;
          const newPageInfos = fetchMoreResult.Page.pageInfo;
          const hasMore = fetchMoreResult.Page.pageInfo.hasNextPage;

          this.showMoreEnabled = hasMore;

          return {
            Page: {
              __typename: previousResult.Page.__typename,
              // Merging the tag list
              pageInfo: [...previousResult.Page.pageInfo, ...newPageInfos],
              media: [...previousResult.Page.media, ...newMedias],
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
