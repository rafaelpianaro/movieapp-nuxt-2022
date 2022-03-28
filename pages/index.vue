<template>
  <div class="home">
    <Hero />

    <div class="container movies">
      <div id="movie-grid" class="movie-grid">
        <div class="movie" v-for="(movie, index) in movies" :key="index">

          <div class="movie-img">
            <img :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`" alt="">
            <p class="review">{{ movie.vote_avarage }}</p>
            <p class="overview">{{ movie.overview }}</p>
          </div>

          <div class="info">
            <p class="title">{{ movie.title.slice(0,25) }} <span v-if="movie.title.length > 25">...</span></p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'IndexPage',
  data() {
    return {
      movies: [],
    }
  },
  async fetch() {
    await this.getMovies()
  },
  methods: {
    async getMovies() {
      const data = axios.get(
        `https://api.themoviedb.org/3/movie/now_playing?api_key=881318e9b461104d3c6d1c0828f90c12&language=en-US&page=1`
      )
      const result = await data
      // console.log('result', result.data)
      result.data.results.forEach((movie) => {
        this.movies.push(movie)
      })
      console.log('array movies',this.movies)
    }
  }
}
</script>
