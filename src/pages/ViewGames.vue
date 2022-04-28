<template>
    <div class="dropdown" v-if="games">
        <button class="dropdownbn">Sort</button>
        <div class="content">
          <h5 class="reverse" @click="reverse">Descending Order</h5>  
        </div>
      </div>
  <div className="container-grid">
    <GameCard v-for="game in games" :key="game.id" :name="game.name" :image="game.background_image" :rating="game.metacritic"/>
  </div>
</template>

<script>
import axios from 'axios'
import GameCard from '../components/GameCard.vue'
const API_KEY = process.env.VUE_APP_KEY

  export default {
    name: 'ViewGames',
    data: () => ({
      games: [],
      clicked: false
    }),
    // props: ['name', 'image'],
    components: {
      GameCard
    },
    mounted() {
      this.getGamesByGenre(this.$route.params.genre_id)
    },
    methods: {
      async getGamesByGenre(genreId) {
        const res = await axios.get(`https://api.rawg.io/api/games?genres=${genreId}&ordering=-metacritic&key=${API_KEY}`)
        this.games = res.data.results
        console.log(this.games)
      },
      reverse() {
        if (this.clicked === false) {
          document.querySelector(".reverse").innerHTML = "Descending Order"
          this.games.reverse()
          this.clicked = true
        } else if (this.clicked === true){
          document.querySelector(".reverse").innerText = "Ascending Order"
          this.games.reverse()
          this.clicked = false
        }
      },
    }
  }
</script>
