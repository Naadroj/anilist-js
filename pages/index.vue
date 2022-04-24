<template>
  <div class="container">
    <show-at breakpoint="mediumAndBelow"> SMALL NAVBAR </show-at>
    <hide-at breakpoint="mediumAndBelow"> BIG NAVBAR </hide-at>
    <br />
    <br />
    <FilterBar />
    <br />
    <br />
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
</template>

<script>
import { showAt, hideAt } from "vue-breakpoints";
export default {
  components: { hideAt, showAt },
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
</style>
