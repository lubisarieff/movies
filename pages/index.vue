<template>
  <div class="container">
    <div v-for="(movie, index) in movies" :key="index">
        <img class="img-fluid" :src="movie.poster_path && `http://image.tmdb.org/t/p/w500/${movie.poster_path}`" :alt="movie.poster_path">
        <p class="text-justify">{{movie.title}}</p> 
        <p class="text-monospace">{{movie.release_date}}</p>        
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      movies: []
    }
  },
  mounted() {
    this.getMovies()
  },
  methods: {
    getMovies() {
      axios.get('https://api.themoviedb.org/3/discover/movie?api_key=eb9ff522676fd1e57fbd5f7ebd4fe38d&language=en-US&sort_by=popularity.desc&page=2&release_date.gte=2020')
        .then(res =>
          res.data.results.forEach(movie =>
            this.movies.push(movie)
          )
        )
        .catch(err =>
          console.log(err)
        )
    }
  }
}
</script>

<style>
.container {
  display: flex;
  flex-wrap: wrap;
}
</style>
