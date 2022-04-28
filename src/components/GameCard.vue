<template>
  <div class="card game-card">
    <div class="image-wrapper">
      <img :src="image" />
    </div>
    <div class="info-wrapper flex-col">
      <h1 class="rating">{{ name }} {{ rating }}</h1>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'GameCard',
    props: ['name', 'image', 'rating']
  }
</script>
