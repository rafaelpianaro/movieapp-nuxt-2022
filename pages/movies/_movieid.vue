<template>
<Loading v-if="$fetchState.pending" />
<div v-else class="container single-movie">
    <NuxtLink class="button" :to="{name : 'index' }">Back</NuxtLink>
    <div class="movie-info">
        <div class="movie-img">
            <img :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`" alt="">
        </div>
        <div class="movie-content">
            <h1>Title: {{ movie.title }}</h1>
            <p class="movie-fact tagline">
                <span>TagLine:</span>{{ movie.tagline }}
            </p>
            <p class="movie-fact">
                <span>Released:</span>
                {{
                    new Date(movie.release_date).toLocaleString('pt-br',{
                    month: 'long',
                    day: 'numeric',
                    year: 'numeric',
                    })
                }}
            </p>
        </div>
    </div>
</div>
</template>

<script>
import axios from "axios"
export default {
    name: 'single-movie',
    data() {
        return {
            movie: null,
        }
    },
    async fetch() {
        await this.getSingleMovie()
    },
    fetchDelay: 1000,
    methods: {
        async getSingleMovie() {
            const data = axios.get(
                `https://api.themoviedb.org/3/movie/${this.$route.params.movieid}?api_key=881318e9b461104d3c6d1c0828f90c12&language=pt-BR`
            )
            const result = await data
            this.movie = result.data
        }
    }
}
</script>

<style lang="scss" scoped>

</style>