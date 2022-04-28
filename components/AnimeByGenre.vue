<template>
  <div>
    <div class="row" v-if="list" id="infinite-list">
      <div
        class="col-12 col-sm-6 col-md-4 col-xl-2"
        v-for="el in list"
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
    <div class="row justify-content-center">
      <b-button
        variant="outline-primary"
        v-if="showMoreEnabled"
        @click="showMore"
        >Show more</b-button
      >
    </div>
  </div>
</template>

<script>
import AnimeByGenre from "../apollo/queries/AnimeByGenre";

export default {
  data() {
    return {
      Page: {
        media: [],
        pageInfo: {
          hasNextPage: true,
        },
      },
      list: [],
      page: 1,
      showMoreEnabled: true,
      pageSize: 48,
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
      result({ data, loading, networkStatus }) {
        data.Page.media.forEach((element) => {
          this.list.push(element);
        });
        console.log(this.list);
      },
    },
  },
  watch: {
    genre(val) {
      this.list = [];
    },
  },
  methods: {
    showMore() {
      this.page++;
      this.$apollo.queries.Page.fetchMore({
        variables() {
          return {
            perPage: this.pageSize,
          };
        },
        updateQuery: (previousResult, { fetchMoreResult }) => {
          const newMedias = fetchMoreResult.Page.media;
          const newPageInfos = fetchMoreResult.Page.pageInfo;
          const hasMore = fetchMoreResult.Page.pageInfo.hasNextPage;

          this.showMoreEnabled = hasMore;

          return {
            Page: {
              __typename: previousResult.Page.__typename,
              pageInfo: [newPageInfos],
              media: [newMedias],
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
