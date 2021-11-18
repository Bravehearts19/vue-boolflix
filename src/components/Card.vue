<template>
    <div class="card_container">  <!-- v-for="(movie) in moviesList" :key="movie.id"  -->
        <span>
            <strong>Titolo:</strong> {{ cardInformation.title }}
        </span>

        <br>

        <span>
            <strong>Titolo originale:</strong> {{ cardInformation.original_title }}
        </span>

        <br>

        <span class="span_with_stars">
            <strong>Voto:</strong> {{ cardInformation.vote_average }}
            <i class="fa fa-star" aria-hidden="true"></i>
            <i class="fa fa-star" aria-hidden="true"></i>
            <i class="fa fa-star" aria-hidden="true"></i>
            <i class="fa fa-star-o" aria-hidden="true"></i>
            <i class="fa fa-star-o" aria-hidden="true"></i>
        </span>

        <br>

        <span class="span_with_image">
            <strong>Lingua:</strong> <img :src="!(languagesFlagsUrlList.hasOwnProperty(cardInformation.original_language)) ? languagesFlagsUrlList.others : languagesFlagsUrlList[cardInformation.original_language]" alt=""> ({{ cardInformation.original_language }})
        </span>

        <br>

        <span class="span_with_image">
            <strong>Trama:</strong> {{ cardInformation.overview }}
        </span>

        <br>

        <!-- <img :src="cardInformation.imagePath" alt=""> -->

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