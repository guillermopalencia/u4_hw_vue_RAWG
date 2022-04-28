<template>
  <div>
    <div class="search">
      <form @submit="getSearchResults">
      <input
        type="text"
        name="search"
        :value="searchQuery"
        placeholder="Search Games"
        @input="handleChange"
      />
      </form>

      <h2>Search Results</h2>
      <section class="search-results container-grid">
        <GameCard v-for="results in searchResults" :key="results.id" :name="results.name" :image="results.background_image" @click="selectGame(results.id)"/>
      </section>
    </div>

    <div class="genres" v-if="!searched">
      <h2>Genres</h2>
      <section class="container-grid">
        <GenreCard v-for="genre in genres" :key="genre.id" :image="genre.image_background" :name="genre.name" @click="selectGenre(genre.id)"/>
      </section>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import GenreCard from '../components/GenreCard.vue'
import GameCard from '../components/GameCard.vue'
const API_KEY = process.env.VUE_APP_KEY

  export default {
    name: 'HomePage',
    components: {
      GenreCard,
      GameCard
    },
    data: () => ({
      genres: [],
      searchQuery: '',
      searchResults: [],
      searched: false
    }),
    mounted() {
      this.getGenres()
    },
    methods: {
      async getGenres() {
        const res = await axios.get(`https://api.rawg.io/api/genres?key=${API_KEY}`)
        this.genres = res.data.results
        console.log(res.data.results)
      },
      async getSearchResults(e){
        e.preventDefault()
        const res = await axios.get(`https://api.rawg.io/api/games?key=${API_KEY}&search=${this.searchQuery}`)
        this.searchResults = res.data.results
        console.log(this.searchResults)
        this.searched = true
      },
      handleChange(event) {
        this.searchQuery = event.target.value
      },
      selectGame(gameId) {
        this.$router.push(`/details/${gameId}`)
        console.log(gameId)
      },
      selectGenre(genreId) {
        this.$router.push(`/genre/${genreId}`)
      }
    }
  }
</script>
