<template>
  <div class="home">
    <Hero />
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
