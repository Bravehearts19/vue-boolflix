<template>
    <li class="my-3">  <!-- v-for="(movie) in moviesList" :key="movie.id"  -->
        {{ cardInformation.title }}

        <br>

        {{ cardInformation.original_title }}

        <br>

        {{ cardInformation.original_language }}
        <img :src="!(languagesFlagsUrlList.hasOwnProperty(cardInformation.original_language)) ? languagesFlagsUrlList.others : languagesFlagsUrlList[cardInformation.original_language]" alt="">

        <br>

        {{ cardInformation.vote_average }}

        <br>

        <img :src="cardInformation.imagePath" alt="">

    </li>
</template>

<script>
export default {
    name: 'Card',
    props: {
        movieOrSeries: Object,
        languagesFlagsUrlList: Object
    },
    data() {
        return {
            startImgUrl: "https://image.tmdb.org/t/p/",
            imgUrlWidth: "w342",
        }
    },
    computed: {
        cardInformation() {
            const cardInformation = {};

            if(this.movieOrSeries.title) {
                cardInformation.title = this.movieOrSeries.title
            } else {
                cardInformation.title = this.movieOrSeries.name
            }

            if(this.movieOrSeries.original_title) {
                cardInformation.original_title = this.movieOrSeries.original_title
            } else {
                cardInformation.original_title = this.movieOrSeries.original_name
            }

            cardInformation.original_language = this.movieOrSeries.original_language;

            cardInformation.vote_average = this.fiveStarVote();

            cardInformation.imagePath = this.cardInformationImagePath();

            return cardInformation
        }
    },
    methods: {
        fiveStarVote() {
            let fiveStarVote = Math.round(this.movieOrSeries.vote_average / 2);
            if (fiveStarVote === 0) {
                fiveStarVote ++;
            }
            return fiveStarVote
        },
        cardInformationImagePath() {
            let cardInformationImagePath = this.startImgUrl + this.imgUrlWidth + this.movieOrSeries.poster_path
            return cardInformationImagePath
        }
    }
}
</script>

<style>

</style>