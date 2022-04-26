<template>
  <div class="container">
    <show-at breakpoint="mediumAndBelow"> SMALL NAVBAR </show-at>
    <hide-at breakpoint="mediumAndBelow"> BIG NAVBAR </hide-at>
    <br />
    <br />
    <div class="row">
      <div class="col-11 col-sm-11 col-md-11 col-lg-11 col-xl-2">
        <h3 class="filter-label">Search</h3>
        <b-form-input size="sm" class="mr-sm-2"></b-form-input>
      </div>
      <hide-at :breakpoints="{ medium: 1200 }" breakpoint="mediumAndBelow">
        <div class="col-2">
          <h3 class="filter-label">Genres</h3>
          <b-form-select
            v-model="selectedGenre"
            :options="options"
            size="sm"
          ></b-form-select>
        </div>
      </hide-at>
      <hide-at :breakpoints="{ medium: 1200 }" breakpoint="mediumAndBelow">
        <div class="col-2">
          <h3 class="filter-label">Year</h3>
          <b-form-select
            v-model="selectedYear"
            :options="fakeOptions"
            size="sm"
          ></b-form-select>
        </div>
      </hide-at>
      <hide-at :breakpoints="{ medium: 1200 }" breakpoint="mediumAndBelow">
        <div class="col-2">
          <h3 class="filter-label">Season</h3>
          <b-form-select
            v-model="selectedSeason"
            :options="fakeOptions"
            size="sm"
          ></b-form-select>
        </div>
      </hide-at>
      <hide-at :breakpoints="{ medium: 1200 }" breakpoint="mediumAndBelow">
        <div class="col-2">
          <h3 class="filter-label">Format</h3>
          <b-form-select
            v-model="selectedFormat"
            :options="fakeOptions"
            size="sm"
          ></b-form-select>
        </div>
      </hide-at>
      <show-at :breakpoints="{ medium: 1200 }" breakpoint="mediumAndBelow">
        breakpoint
      </show-at>
    </div>
    <br />
    <br />
    <div id="homeDisplay" v-if="selectedGenre == null">
      <div class="row">
        <div class="col-12">
          <TrendingNow />
        </div>
      </div>
      <br />
      <div class="row">
        <div class="col-12">
          <PopularThisSeason />
        </div>
      </div>
      <br />
      <div class="row">
        <div class="col-12">
          <UpcomingNextSeason />
        </div>
      </div>
      <br />
      <div class="row">
        <div class="col-12">
          <AllTimePopular />
        </div>
      </div>
      <br />
      <div class="row">
        <div class="col-12">
          <Top100Anime />
        </div>
      </div>
    </div>
    <div id="listDisplay" v-else>
      <AnimeByGenre :genre="selectedGenre" />
    </div>
  </div>
</template>

<script>
import { showAt, hideAt } from "vue-breakpoints";
export default {
  components: { hideAt, showAt },
  data() {
    return {
      selectedGenre: null,
      selectedYear: null,
      selectedSeason: null,
      selectedFormat: null,
      options: [
        { value: null, text: "Any", disabled: true },
        { value: "Action", text: "Action" },
        { value: "Comedy", text: "Comedy" },
        { value: "Fantasy", text: "Fantasy" },
        { value: "Music", text: "Music" },
      ],
      fakeOptions: [{ value: null, text: "Any" }],
    };
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Overpass:wght@100;200;700&display=swap");

body {
  background-color: #e5ebf1;
  font-family: "Overpass", sans-serif;
  color: #26343f;
}

h2 {
  font-size: 1rem;
  font-weight: 700;
  font-weight: bold;
  margin-bottom: 20px;
}

.card-body {
  padding: 0 !important;
}

.media-title {
  font-size: 0.8rem;
  font-weight: bold;
}

.filter-label {
  font-size: 0.9rem;
  font-weight: bold;
  margin-bottom: 4vh;
}

.form-control {
  height: 2rem !important;
  font-size: 0.8rem !important;
}

a{
  color: #516170 !important;
}

a:hover{
  text-decoration: none !important;
  color: #EF5D5D !important;
}
</style>
