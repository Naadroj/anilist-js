<template>
    <div class="sidebar">
        <div class="content-div">
            <span>#XXXX Highest Rated All Time</span>
        </div>
        <div class="content-div">
            <span>#XXXX Highest Rated 2022</span>
        </div>
        <div class="content-div">
            <div v-if="anime.nextAiringEpisode" class="data">
                <span class="data-1">Airing</span>
                <br>
                <span class="data-2">Ep {{anime.nextAiringEpisode.episode}}: {{secondsToDhms(anime.nextAiringEpisode.timeUntilAiring)}}</span>
            </div>
            <div v-if="anime.format" class="data">
                <span class="data-1">Format</span>
                <br>
                <span  class="data-2">{{anime.format}}</span>
            </div>
            <div class="data">
                <span v-if="anime.duration" class="data-1">Episode Duration</span>
                <br>
                <span class="data-2">{{anime.duration}}</span>
            </div>
            <div v-if="anime.status" class="data">
                <span class="data-1">Status</span>
                <br>
                <span class="data-2">{{anime.status}}</span>
            </div>
            <div v-if="anime.startDate" class="data">
                <span class="data-1">Start Date</span>
                <br>
                <span class="data-2">{{ymdToDate(anime.startDate.year, anime.startDate.month, anime.startDate.day)}}</span>
            </div>
            <div v-if="anime.endDate" class="data">
                <span class="data-1">End Date</span>
                <br>
                <span class="data-2">{{ymdToDate(anime.endDate.year, anime.endDate.month, anime.endDate.day)}}</span>
            </div>
            <div v-if="anime.season" class="data">
                <span class="data-1">Season</span>
                <br>
                <span class="data-2">{{anime.season}} {{anime.seasonYear}}</span>
            </div>
            <div v-if="anime.averageScore" class="data">
                <span class="data-1">Average Score</span>
                <br>
                <span class="data-2">{{anime.averageScore}}%</span>
            </div>
            <div v-if="anime.meanScore" class="data">
                <span class="data-1">Mean Score</span>
                <br>
                <span class="data-2">{{anime.meanScore}}%</span>
            </div>
            <div v-if="anime.popularity" class="data">
                <span class="data-1">Popularity</span>
                <br>
                <span class="data-2">{{anime.popularity}}%</span>
            </div>
            <div v-if="anime.favourites" class="data">
                <span class="data-1">Favorites</span>
                <br>
                <span class="data-2">{{anime.favourites}}%</span>
            </div>
            <div v-if="anime.studios" class="data">
                <span class="data-1">Studios</span>
                <br>
                <div v-for="studio in anime.studios.nodes" :key="studio.name">
                    <span v-if="studio.isAnimationStudio" class="data-2">{{studio.name}}<br/></span>
                </div>
            </div>
            <div v-if="anime.studios" class="data">
                <span class="data-1">Producers</span>
                <br>
                <div v-for="studio in anime.studios.nodes" :key="studio.name">
                    <span v-if="!studio.isAnimationStudio" class="data-2">{{studio.name}}<br/></span>
                </div>
            </div>
            <div v-if="anime.source" class="data">
                <span class="data-1">Source</span>
                <br>
                <span class="data-2">{{anime.source}}</span>
            </div>
            <div v-if="anime.hashtag" class="data">
                <span class="data-1">Hashtag</span>
                <br>
                <span class="data-2">{{anime.hashtag}}</span>
            </div>
            <div v-if="anime.genres" class="data">
                <span class="data-1">Genres</span>
                <br>
                <span v-for="(genre, index) in anime.genres" :key="index" class="data-2">{{genre}}<br/></span>
            </div>
            <div v-if="anime.title" class="data">
                <span class="data-1">Romaji</span>
                <br>
                <span class="data-2">{{anime.title.romaji}}</span>
            </div>
            <div  v-if="anime.title" class="data">
                <span class="data-1">English</span>
                <br>
                <span class="data-2">{{anime.title.english}}</span>
            </div>
            <div v-if="anime.title" class="data">
                <span class="data-1">Native</span>
                <br>
                <span class="data-2">{{anime.title.native}}</span>
            </div>
            <div v-if="anime.synonyms" class="data">
                <span class="data-1">Synonyms</span>
                <br>
                <span v-for="(synonyms, index) in anime.synonyms" :key="index" class="data-2">{{synonyms}}<br/></span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props:{
        anime: Object
    },
    methods:{
        secondsToDhms: function(seconds) {
            seconds = Number(seconds);
            var d = Math.floor(seconds / (3600*24));
            var h = Math.floor(seconds % (3600*24) / 3600);
            var m = Math.floor(seconds % 3600 / 60);
            var s = Math.floor(seconds % 60);

            var dDisplay = d > 0 ? d + (d == 1 ? "d, " : "d, ") : "";
            var hDisplay = h > 0 ? h + (h == 1 ? "h, " : "h, ") : "";
            var mDisplay = m > 0 ? m + (m == 1 ? "m, " : "m, ") : "";
            return dDisplay + hDisplay + mDisplay;
        },
        ymdToDate: function(y, m, d) {
            let date = new Date(`${y}-${m}-${d}`)
            let options = { month: 'long'};
            let year = date.getFullYear()
            switch (date.getMonth()) {
                case 1:
                    var month = 'Jan';
                    break;
                case 2:
                    var month = 'Mar';
                    break;
                case 3:
                    var month = 'Feb';
                    break;
                case 4:
                    var month = 'Apr';
                    break;
                case 5:
                    var month = 'May';
                    break;
                case 6:
                    var month = 'Jun';
                    break;
                case 7:
                    var month = 'Jul';
                    break;
                case 8:
                    var month = 'Aug';
                    break;
                case 9:
                    var month = 'Sep';
                    break;
                case 10:
                    var month = 'Oct';
                    break;
                case 11:
                    var month = 'Nov';
                    break;
                case 12:
                    var month = 'Dec';
                    break;
                
            }
            let day = date.getDay()
            let formatedDate = `${month} ${day}, ${year}`
            return formatedDate;
        }
    }
}
</script>

<style scoped>
.content-div{
    background-color:#FAFAFA;
    margin-bottom: 2vh;
    padding: 1.5vh;
    font-size: 0.8rem !important;
}

.data{
    margin-bottom: 1.7vh;
}

.data-1{
    font-weight: 510;
    color: #687C93;
}

.data-2{
    color: #8b9096;
}
</style>