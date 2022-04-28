<template>
  <div id="__layout">
    <Navbar />
    <div class="page-content">
      <div class="banner" :style="getUrl(Media.bannerImage)"></div>
      <div class="header-wrap">
        <div class="row">
          <div class="col-4 col-sm-4 col-md-1 col-xl-1"></div>
          <div class="col-4 col-sm-4 col-md-2 col-xl-2">
            <img :src="Media.coverImage.large" class="cover" />
          </div>
          <div class="col-12 col-sm-12 col-md-7 col-xl-7 title-and-desc">
            <h1>{{ Media.title.romaji }}</h1>
            <p ref="description"></p>
          </div>
        </div>
        <div class="row justify-content-center infos-options">
          <b-form-group v-slot="{ ariaDescribedby }">
            <b-form-radio-group
              id="infos"
              v-model="selectedInfo"
              :options="infosOptions"
              :aria-describedby="ariaDescribedby"
              name="radio-options"
            ></b-form-radio-group>
          </b-form-group>
        </div>
      </div>

      <div class="content">
        <div class="row">
          <div class="col-0 col-sm-0 col-md-1 col-xl-1"></div>
          <div class="col-0 col-sm-0 col-md-2 col-xl-2">
            <SideBar :anime="Media" />
          </div>
          <div class="col-12 col-sm-12 col-md-8 col-xl-8">
            <Overview v-if="selectedInfo == 'overview'" />
            <Characters v-else-if="selectedInfo == 'characters'" />
            <Staff v-else-if="selectedInfo == 'staff'" />
            <Stats v-else-if="selectedInfo == 'stats'" />
            <Social v-else />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import OneAnime from "../apollo/queries/OneAnime";

export default {
  data() {
    return {
      Media: {
        title: [],
        description: "",
        coverImage: {
          large: "",
        },
        bannerImage: "",
      },
      media: {},
      selectedInfo: "overview",
      infosOptions: [
        { text: "Overview", value: "overview" },
        { text: "Characters", value: "characters" },
        { text: "Staff", value: "staff" },
        { text: "Stats", value: "stats" },
        { text: "Social", value: "social" },
      ],
      setDescriptionBool: 0,
    };
  },
  apollo: {
    Media: {
      query: OneAnime,
      variables() {
        return {
          id: this.$route.params.anime,
        };
      },
    },
  },
  mounted: function () {
    this.$refs.description.innerHTML = this.Media.description;
  },
  methods: {
    getUrl: function (el) {
      return `background-image: url(${el}); 
            height:40vh;
            background-position: 50% 35%;
            background-repeat: no-repeat;
            background-size: cover;
            height: 50vh;
            width: auto;`;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Overpass:wght@100;200;700&display=swap");

body {
  background-color: #e5ebf1;
}

.page-content {
  font-family: "Overpass", sans-serif;
  color: #26343f;
}

.row {
  margin-right: 0px !important;
  margin-left: 0px !important;
}

.cover {
  background-color: rgba(212, 230, 245, 0.5);
  border-radius: 2px;
  box-shadow: 0 0 29px rgb(49 54 68 / 25%);
  margin-top: -125px;
  width: 100%;
}

h1 {
  font-size: 1.2rem;
  font-weight: 400;
}

.infos-options {
  margin-top: 2rem;
}

.title-and-desc {
  margin-top: 2rem;
}

.header-wrap {
  background-color: #fafafa;
}

.content {
  padding-top: 4vh;
  background-color: #edf1f5;
}

a {
  color: #516170 !important;
}

a:hover {
  text-decoration: none !important;
  color: #ef5d5d !important;
}
</style>