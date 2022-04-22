<template>
  <div class="container">
    <ul>
      <li v-for="media in Page.media" :key="media.id">
        <!-- {{ media.title.english }} -->
        <img src="{{media.}}" alt="" />
      </li>
      <!-- <p v-if="test">
      {{ Page }}
      test
      </p> -->
    </ul>
  </div>
</template>

<script>
import gql from "graphql-tag";

export default {
  apollo: {
    Page: gql`
      query ($page: Int, $perPage: Int, $search: String) {
        Page(page: $page, perPage: $perPage) {
          pageInfo {
            total
            perPage
          }
          media(search: $search, type: ANIME, sort: ID) {
            id
            title {
              romaji
              english
              native
            }
            type
            genres
          }
        }
      }
    `,
  },
};
</script>

<style scoped>
</style>
