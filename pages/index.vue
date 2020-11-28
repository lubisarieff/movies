<template>
  <div class="mt-4">
    <div class="container">
      <h1>Movies</h1>
      <div class="card-columns">
        <div class="card" v-for="movie in movies" :key="movie.key">
          <img class="card-img" :src="movie.poster_path && `http://image.tmdb.org/t/p/w500/${movie.poster_path}`" :alt="movie.poster_path">
          <div class="card-body">
            <p class="card-text">{{movie.title}}</p>
          </div>
        </div>
      </div>
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
.container-fluid {
  display: flex;
  flex-wrap: wrap;
}
.img-fluid {
}
</style>
