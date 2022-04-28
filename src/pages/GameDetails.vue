<template>
<button @click="backHome">
  Home
</button>
  <div class="game-content">
    <section class="image-container">
      <div>
        <img :src="image" />
        <h1>{{ name }}</h1>
      </div>
    </section>
    <section class="details">
      <div class="flex-row space"></div>
      <div>
        <h3>{{ gameDetails }}</h3>
      </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios'
const API_KEY = process.env.VUE_APP_KEY

  export default {
    name: 'GameDetails',
    props: ['route'] 
    ,
    data: () => ({
      gameId: null,
      gameDetails: null,
      image: null,
      title: null,
      rating: null
    }),
    mounted: function() {
      this.getGameDetails(this.$route.params.game_id)
      console.log(this.$route.params.game_id)
    },
    methods: {
      async getGameDetails(gameId) {
        const res = await axios.get(`https://api.rawg.io/api/games/${gameId}?key=${API_KEY}`)
        this.gameDetails = res.data.description
        this.image = res.data.background_image
        this.name = res.data.name
        this.rating = res.data.ratings_count
        console.log(res.data)
      },
      backHome() {
        this.$router.push(`/`)
      }
    }
  }
</script>
