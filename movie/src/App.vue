<template>
  <div id="app">
    <div class="container">
      <!-- 1-3. 호출하시오. 
        필요한 경우 props를 데이터를 보내줍니다.
      -->
      <MovieList :movielist="movielist" :genrelist="genrelist" />
    </div>
  </div>
</template>

<script>
const axios = require("axios");
// 1-1. 저장되어 있는 MovieList 컴포넌트를 불러오고,
import MovieList from "./components/movies/MovieList";

export default {
  name: "app",
  // 1-2. 아래에 등록 후
  props: {
    genre: String
  },
  components: {
    MovieList
  },
  data() {
    return {
      // 활용할 데이터를 정의하시오.
      movielist: [],
      genrelist: []
    };
  },
  mounted() {
    // 0. mounted 되었을 때,
    // 1) 제시된 URL로 요청을 통해 data의 movies 배열에 해당 하는 데이터를 넣으시오.
    axios
      .get(
        "https://gist.githubusercontent.com/BuankerC/c03105ea244c2511da556c5b41ad8f56/raw/de424312e0ca08695b6148b00637d31934d50e4e/movie.json"
      )
      .then(response => {
        const movielist = response.data;
        this.movielist = movielist;
      });
    // 2) 제시된 URL로 요청을 통해 data의 genres 배열에 해당 하는 데이터를 넣으시오.
    axios
      .get(
        "https://gist.githubusercontent.com/BuankerC/76207402aad082fa113366ca5f62bfed/raw/d13a6dfd5d6a8dad2b514002ba5462b1f86f29ef/genre.json"
      )
      .then(response => {
        const genrelist = response.data;
        this.genrelist = genrelist;
      });
    // axios는 위에 호출되어 있으며, node 설치도 완료되어 있습니다.
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
