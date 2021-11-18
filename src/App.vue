<template>
    <div id="app">
      <Header :apiKey="apiKey" :apiUrl="apiUrl" @onSearchSeries="onSearchSeries" @onSearchMovies="onSearchMovies" />
      
      <ul>
        <Card :movieOrSeries="movie" :languagesFlagsUrlList="languagesFlagsUrlList" v-for="(movie) in moviesList" :key="movie.id"/>
      </ul>
      
      <ul>
        <Card :movieOrSeries="series" :languagesFlagsUrlList="languagesFlagsUrlList" v-for="(series) in seriesList" :key="series.id"/>
      </ul>
    </div>
</template>

<script>
import Card from './components/Card.vue';
import Header from './components/Header.vue';


export default {
  name: 'App',
  components: {
    Card,
    Header,
  },
  data() {
    return {
      apiUrl: "https://api.themoviedb.org/3/",
      apiKey: "979a156d8babee2a3b870e7e13464235",
      languagesFlagsUrlList: {
        en: "https://cdn-icons-png.flaticon.com/128/197/197374.png",
        it: "https://cdn-icons-png.flaticon.com/128/197/197626.png",
        es: "https://cdn-icons-png.flaticon.com/128/197/197593.png",
        fr: "https://cdn-icons-png.flaticon.com/128/197/197560.png",
        de: "https://cdn-icons-png.flaticon.com/128/197/197571.png",
        others: "https://cdn-icons-png.flaticon.com/128/744/744502.png"
      },
      moviesList: [],
      seriesList: [],
    }
  },
  methods: {
    onSearchSeries(seriesList) {
      this.seriesList = seriesList;
    },
    onSearchMovies(moviesList) {
      this.moviesList = moviesList;
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
