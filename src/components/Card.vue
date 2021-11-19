<template>
    <div class="card_container" @mouseover="showInformation = true" @mouseleave="showInformation = false">  

        <img v-if="!showInformation" :src="movieOrSeries.poster_path == null ? 'https://www.inixgroup.com/wp-content/uploads/2020/12/placeholder.png' : cardInformation.imagePath" alt="">
        
        <div class="spans_container" v-else>
            <span>
                <strong>Titolo:</strong> {{ cardInformation.title }}
            </span>

            <span v-if="cardInformation.title !== cardInformation.original_title">
                <strong>Titolo originale:</strong> {{ cardInformation.original_title }}
            </span>

            <span class="span_with_stars">
                <strong class="me-2">Voto:</strong> 
                <i class="fa fa-star" aria-hidden="true" v-for="num in cardInformation.vote_average" :key="'star_' + num"></i>
                <i class="fa fa-star-o" aria-hidden="true" v-for="n in 5 - cardInformation.vote_average" :key="'empty_star_' + n"></i>
            </span>

            <span class="span_with_image">
                <strong class="me-2">Lingua:</strong> <img :src="!(languagesFlagsUrlList.hasOwnProperty(cardInformation.original_language)) ? languagesFlagsUrlList.others : languagesFlagsUrlList[cardInformation.original_language]" alt=""> ({{cardInformation.original_language}})
            </span>

            <span class="span_with_image" v-if="cardInformation.overview !== ''">
                <strong>Trama:</strong> {{ cardInformation.overview }}
            </span>
        </div>
    </div>
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
            showInformation: false,
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

            cardInformation.overview = this.movieOrSeries.overview;

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