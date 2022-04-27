<template>
  <div class="informations">
    <div class="info-section">
      <span class="section-title">Characters</span>
      <div class="section-content">
        <div class="row justify-content-between">
          <div
            class="col-5 char-card"
            v-for="(character, index) in Media.characters.edges"
            :key="index"
          >
            <div class="row">
              <div
                class="col-2 character-image"
                :style="getUrl(character.node.image.large)"
              ></div>
              <div class="col-4">
                <span class="name">{{ character.node.name.full }}</span>
                <br />
                <span class="role to-lowercase">{{ character.role }}</span>
              </div>
              <div
                class="col-4"
                v-for="actor in character.voiceActors.slice(0, 1)"
                :key="actor.id"
              >
                <span class="name">{{ actor.name.full }}</span>
                <br />
                <span class="language">{{ actor.languageV2 }}</span>
              </div>
              <div
                class="col-2 character-image"
                :style="getUrl(actor.image.medium)"
                v-for="actor in character.voiceActors.slice(0, 1)"
                :key="actor.id"
              ></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import OverviewAnime from "../../apollo/queries/CharactersAnime.gql";

export default {
  data() {
    return {
      Media: {
        characters: {
          edges: [],
        },
      },
    };
  },
  apollo: {
    Media: {
      query: OverviewAnime,
      variables() {
        return {
          id: this.$route.params.anime,
        };
      },
    },
  },
  methods: {
    getUrl: function (el) {
      return `background-image: url(${el});`;
    },
  },
};
</script>

<style>
.to-lowercase {
  text-transform: lowercase;
  display: inline-block;
}

.to-lowercase:first-letter {
  text-transform: uppercase;
}

.section-title {
  font-size: 1rem;
  color: #2b333b;
  font-weight: bold;
}

.char-card {
  background-color: #fafafa;
  border-radius: 5px;
  text-align: left;
  min-height: 80px;
  box-shadow: 0 14px 30px rgba(var(--color-shadow-blue), 0.15),
    0 4px 4px rgba(var(--color-shadow-blue), 0.05);
  margin: 3vh 0vh 3vh;
}

.character-image {
  height: 80px;
  width: auto;
  background-position: 50% 35%;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 50%;
}

.name {
  font-size: 0.8rem;
  color: #2b333b;
}

.role {
  font-size: 0.7rem;
  color: #2b333b;
  /* position: absolute;
    bottom: 0px; */
}

.language {
  font-size: 0.7rem;
  color: #2b333b;
  /* position: absolute;
    bottom: 0px; */
}

.staff-card {
  background-color: #fafafa;
  border-radius: 5px;
  text-align: left;
  min-height: 80px;
  box-shadow: 0 14px 30px rgba(var(--color-shadow-blue), 0.15),
    0 4px 4px rgba(var(--color-shadow-blue), 0.05);
  margin: 3vh 0vh 3vh;
}
</style>