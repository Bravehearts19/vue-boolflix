<template>
    <header class="container-fluid d-flex align-items-center py-3 m-0">
        <h3 class="text-danger">BOOLFLIX</h3>
        <div class="ms-auto d-flex align-items-center">
            <input type="text" placeholder="Cerca qui film o serie tv" v-model="searchedText" class="d-inline-block" @keydown.enter="onSearchButtonClick()">
            <button type="button" class="btn btn-danger ms-3" @click="onSearchButtonClick()">Cerca</button>
        </div>
    </header>
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