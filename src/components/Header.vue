<template>
    <div class="container-fluid">
        <div class="d-flex align-items-center">
            <h3 class="text-danger">BOOLFLIX</h3>
            <div class="ms-auto">
                <input type="text" placeholder="Scrivi qui il film o la serie tv che sei interessato a vedere" v-model="searchedText" class="w-50 d-inline-block" @keydown.enter="onSearchButtonClick()">
                <button type="button" class="btn btn-primary ms-3" @click="onSearchButtonClick()">Cerca</button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'Header',
    props: {
        apiKey: String,
        apiUrl: String,
    },
    data() {
        return {
            moviesList: [],
            seriesList: [],
            searchedText: "",
        }
    },
    methods: {
    searchQuery(url, textToSearch) {
        axios.get(this.apiUrl + url, {
            params: {
                api_key: this.apiKey,
                query: textToSearch,
                language: "it",
            },
        })
        .then((resp) => {
            if(url.includes("tv")){
                this.seriesList = resp.data.results;
                this.$emit("onSearchSeries", this.seriesList)
            } else if(url.includes("movie")) {
                this.moviesList = resp.data.results;
                this.$emit("onSearchMovies", this.moviesList)
            }
        });
    },
    onSearchButtonClick() {
      this.searchQuery("search/movie", this.searchedText)
      this.searchQuery("search/tv", this.searchedText)
    }
  },
}
</script>

<style>

</style>