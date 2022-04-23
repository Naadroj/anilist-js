<template>
  <div>
    <h2>TOP 100 ANIME</h2>
    <div class="row">
      <div
        class="col-12"
        v-for="(el, index) in Page.media.slice(0, maxElems)"
        :key="el.id"
      >
        <div class="row">
          <div class="col-1">#{{ index + 1 }}</div>
          <div class="col-11 top-100">
            <b-card
              :img-src="el.coverImage.large"
              img-alt="Card image"
              img-left
              style="padding: 1%"
              class="mb-3"
            >
              <div class="row top-100-container">
                <div class="col-6">
                  <span>{{ el.title.romaji }}</span>
                  <div>
                    <span
                      v-for="(tag, index) in el.genres.slice(0, maxTags)"
                      :key="index"
                      class="top-100-tags"
                      >{{ tag }}</span
                    >
                    <!-- <span>{{ el.genres }}</span> -->
                  </div>
                </div>
                <div class="col-2 stats">
                  <!-- <FontAwesomeIcon icon="fa-solid fa-face-smile" /> -->
                  <span class="smiley">:)</span>
                  <div>
                    <span> {{ el.averageScore }}% </span>
                    <br />
                    <span> {{ el.popularity }} users </span>
                  </div>
                </div>
                <div class="col-2">
                  <span class="to-lowercase">{{ el.format }}</span>
                  <br />
                  <span v-if="el.format == 'MOVIE'">{{
                    timeConvert(el.duration)
                  }}</span>
                  <span v-else> {{ el.episodes }} episodes </span>
                </div>
                <div class="col-2">
                  <span class="to-lowercase"
                    >{{ el.season }} {{ el.seasonYear }}</span
                  >
                  <br />
                  <span class="to-lowercase">{{ el.status }}</span>
                </div>
              </div>
            </b-card>
          </div>
        </div>
        <!-- <b-card
          :img-src="el.coverImage.extraLarge"
          :img-alt="el.title.romaji"
          class="mb-2"
        >
        </b-card> -->
        <span class="media-title">
          {{ el.title.romaji }}
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import gql from "graphql-tag";
import Top100Anime from "../apollo/queries/Top100Anime";
export default {
  data() {
    return {
      maxElems: 10,
      maxTags: 5,
    };
  },
  apollo: {
    Page: {
      query: Top100Anime,
      variables: {},
    },
  },
  methods: {
    timeConvert: function (n) {
      let num = n;
      let hours = num / 60;
      let rhours = Math.floor(hours);
      let minutes = (hours - rhours) * 60;
      let rminutes = Math.round(minutes);
      return rhours + " hour(s), " + rminutes + " min(s).";
    },
  },
};
</script>

<style>
.top-100 {
  background-color: #e5ebf1;
  border-radius: 5px;
  text-align: left;
  min-height: 80px;
  box-shadow: 0 14px 30px rgba(var(--color-shadow-blue), 0.15),
    0 4px 4px rgba(var(--color-shadow-blue), 0.05);
}

.top-100-container {
  margin: 1%;
}

.top-100-tags {
  margin-left: 1%;
  margin-right: 1%;
  padding-left: 0.4rem;
  padding-right: 0.4rem;
  padding-top: 0.1rem;
  padding-bottom: 0.1rem;
  /* padding: 0 8px; */
  border: solid 0px transparent;
  /* border-radius: 0%; */
  background-color: red;
  color: #e5ebf1;
  border-radius: 10px;
  font-size: 0.8rem;
  font-weight: bold;
  text-transform: lowercase;
}

.card-img-left {
  max-width: 3.5vw;
}

.stats {
  display: flex;
}

.smiley {
  margin-right: 2%;
  color: rgb(8, 209, 8);
}

.to-lowercase {
  text-transform: lowercase;
  display: inline-block;
}

.to-lowercase:first-letter {
  text-transform: uppercase;
}
</style>
