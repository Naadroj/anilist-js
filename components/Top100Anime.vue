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
          <div class="col-1 top-number">#{{ index + 1 }}</div>

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
                  <NuxtLink :to="el.id.toString()">
                    <span v-if="el.title.romaji.length <= 35">
                      {{ el.title.romaji }}
                    </span>
                    <span v-else>
                      {{ el.title.romaji.slice(0, 35) + "..." }}
                    </span>
                  </NuxtLink>
                  <div>
                    <span
                      v-for="(tag, i) in el.genres.slice(0, 4)"
                      :key="i"
                      class="top-100-tags"
                      :style="setColor(index)"
                      >{{ tag }}</span
                    >
                  </div>
                </div>
                <div class="col-2 stats">
                  <span class="smiley">:)</span>
                  <div>
                    <span class="score"> {{ el.averageScore }}% </span>
                    <br />
                    <span class="popularity"> {{ el.popularity }} users </span>
                  </div>
                </div>
                <div class="col-2">
                  <span class="to-lowercase format">{{ el.format }}</span>
                  <br />
                  <span class="duration" v-if="el.format == 'MOVIE'">{{
                    timeConvert(el.duration)
                  }}</span>
                  <span class="duration" v-else>
                    {{ el.episodes }} episodes
                  </span>
                </div>
                <div class="col-2">
                  <span class="to-lowercase season-year"
                    >{{ el.season }} {{ el.seasonYear }}</span
                  >
                  <br />
                  <span class="to-lowercase status">{{ el.status }}</span>
                </div>
              </div>
            </b-card>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Top100Anime from "../apollo/queries/Top100Anime";
export default {
  data() {
    return {
      Page: {
        media: [],
      },
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
    setColor: function(index){
      const bgColorArray = [
        '#EF5D5D',
        '#3480EA',
        '#E34F85',
        '#E0D59E',
        '#E0D59E',
        '#8A2C0F',
        '#E34F85',
        '#FFF280',
        '#EBB62D',
        '#6EC8F2'
      ];
      const colorArray = [
        '#FAFAFA',
        '#FAFAFA',
        '#FAFAFA',
        '#9F4A16',
        '#786C47',
        '#FAFAFA',
        '#FAFAFA',
        '#AF4F18',
        '#9F4A16',
        '#3F7FA9'
      ];
      let cssRule = `background-color: ${bgColorArray[index]}; color: ${colorArray[index]};`
      return cssRule;
    }
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

.top-number{
  font-size: 1.5rem;
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
  border: solid 0px transparent;
  background-color: red;
  color: #e5ebf1;
  border-radius: 10px;
  font-size: 0.8rem;
  font-weight: bold;
  text-transform: lowercase;
}

.card-img-left {
  max-width: 3.5vw;
  height: 100%;
}

.stats {
  display: flex;
}

.duration {
  font-size: 0.8rem;
}

.format {
  font-size: 0.9rem;
  font-weight: bold;
}

.status {
  font-size: 0.8rem;
}

.score {
  font-size: 0.9rem;
  font-weight: bold;
}

.popularity {
  font-size: 0.8rem;
}

.season-year {
  font-size: 0.9rem;
  font-weight: bold;
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
