<template>
    <div class="informations">
       <div class="info-section">
            <span class="section-title">Staff</span>
            <div class="section-content">
                <div class="row justify-content-between">
                    <div class="col-5 staff-card" v-for="(staff, index) in Media.staff.edges" :key="index">
                        <div class="row">
                            <div class="col-2 character-image" :style="getUrl(staff.node.image.large)"></div>
                            <div class="col-10">
                                <span class="name">{{staff.node.name.full}}</span>
                                <br>
                                <span class="role">{{staff.role}}</span>
                            </div>
    
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import StaffAnime from '../../apollo/queries/StaffAnime.gql'

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
            query: StaffAnime,
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
}
</script>

<style>
.section-title{
    font-size: 1rem;
    color: #2b333b;
    font-weight: bold;
}

.char-card{
    background-color: #FAFAFA;
    border-radius: 5px;
    text-align: left;
    min-height: 80px;
    box-shadow: 0 14px 30px rgba(var(--color-shadow-blue), 0.15),
    0 4px 4px rgba(var(--color-shadow-blue), 0.05);
    margin: 3vh 0vh 3vh;
}

.character-image{
    height: 80px;
    width: auto;
    background-position: 50% 35%;
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 50%;
}

.name{
    font-size: 0.8rem;
    color: #2b333b;
}

.role{
    font-size: 0.7rem;
    color: #2b333b;
    position: absolute;
    bottom: 0px;
}

.staff-card{
    background-color: #FAFAFA;
    border-radius: 5px;
    text-align: left;
    min-height: 80px;
    box-shadow: 0 14px 30px rgba(var(--color-shadow-blue), 0.15),
    0 4px 4px rgba(var(--color-shadow-blue), 0.05);
    margin: 3vh 0vh 3vh;
}
</style>