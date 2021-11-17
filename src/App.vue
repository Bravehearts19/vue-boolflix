<template>
    <div id="app">
      <input type="text" placeholder="Scrivi qui il film o la serie tv che sei interessato a vedere" v-model="searchedText" class="w-50 d-inline-block" @keydown.enter="onSearchButtonClick()">
      <button type="button" class="btn btn-primary ms-3" @click="onSearchButtonClick()">Cerca</button>
      <ul>
        <Card :movieOrSeries="movie" :languagesFlagsUrlList="languagesFlagsUrlList" v-for="(movie) in moviesList" :key="movie.id"/>
      </ul>
      
      <ul>
        <Card :movieOrSeries="series" :languagesFlagsUrlList="languagesFlagsUrlList" v-for="(series) in seriesList" :key="series.id"/>
      </ul>
    </div>
</template>

<script>
import axios from 'axios';
import Card from './components/Card.vue';


export default {
  name: 'App',
  components: {
    Card,
  },
  data() {
    return {
      apiUrl: "https://api.themoviedb.org/3/",
      apiKey: "979a156d8babee2a3b870e7e13464235",
      moviesList: [],
      seriesList: [],
      languagesFlagsUrlList: {
        en: "https://cdn-icons-png.flaticon.com/128/197/197374.png",
        it: "https://cdn-icons-png.flaticon.com/128/197/197626.png",
        es: "https://cdn-icons-png.flaticon.com/128/197/197593.png",
        fr: "https://cdn-icons-png.flaticon.com/128/197/197560.png",
        de: "https://cdn-icons-png.flaticon.com/128/197/197571.png",
        others: "https://cdn-icons-png.flaticon.com/128/744/744502.png"
      },
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
        } else if(url.includes("movie")) {
          this.moviesList = resp.data.results;
        }
      });
    },
    onSearchButtonClick() {
      this.searchQuery("search/movie", this.searchedText)
      this.searchQuery("search/tv", this.searchedText)
    }
  },
  mounted() {
    
  }
}
</script>

<style lang="scss">
@import "./styles/app.scss";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
