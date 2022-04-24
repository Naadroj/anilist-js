<template>
  <div class="row">
    <div class="col-11 col-sm-11 col-md-11 col-lg-11 col-xl-2">
      <h3 class="filter-label">Search</h3>
      <b-form-input size="sm" class="mr-sm-2"></b-form-input>
    </div>
    <hide-at :breakpoints="{ medium: 1200 }" breakpoint="mediumAndBelow">
      <div class="col-2">
        <h3 class="filter-label">Genres</h3>
        <b-form-input list="my-list-1" placeholder="Any"></b-form-input>

        <datalist id="my-list-1">
          <option v-for="(genre, index) in genres" :key="index">
            {{ genre }}
          </option>
        </datalist>
      </div>
    </hide-at>
    <hide-at :breakpoints="{ medium: 1200 }" breakpoint="mediumAndBelow">
      <div class="col-2">
        <h3 class="filter-label">Year</h3>
        <b-form-input list="my-list-2" placeholder="Any"></b-form-input>

        <datalist id="my-list-2">
          <option v-for="(fake, index) in fakeOptions" :key="index">
            {{ fake }}
          </option>
        </datalist>
      </div>
    </hide-at>
    <hide-at :breakpoints="{ medium: 1200 }" breakpoint="mediumAndBelow">
      <div class="col-2">
        <h3 class="filter-label">Season</h3>
        <b-form-input list="my-list-2" placeholder="Any"></b-form-input>

        <datalist id="my-list-2">
          <option v-for="(fake, index) in fakeOptions" :key="index">
            {{ fake }}
          </option>
        </datalist>
      </div>
    </hide-at>
    <hide-at :breakpoints="{ medium: 1200 }" breakpoint="mediumAndBelow">
      <div class="col-2">
        <h3 class="filter-label">Format</h3>
        <b-form-input list="my-list-2" placeholder="Any"></b-form-input>

        <datalist id="my-list-2">
          <option v-for="(fake, index) in fakeOptions" :key="index">
            {{ fake }}
          </option>
        </datalist>
      </div>
    </hide-at>
    <show-at :breakpoints="{ medium: 1200 }" breakpoint="mediumAndBelow">
      breakpoint
    </show-at>
  </div>
</template>

<script>
import { showAt, hideAt } from "vue-breakpoints";
export default {
  components: { hideAt, showAt },
  data() {
    return {
      selected: null,
      genres: ["Action", "Comedy", "Fantasy", "Music"],
      fakeOptions: [],
    };
  },
};
</script>

<style>
.filter-label {
  font-size: 0.9rem;
  font-weight: bold;
  margin-bottom: 4vh;
}

.form-control {
  height: 2rem !important;
  font-size: 0.8rem !important;
}
</style>