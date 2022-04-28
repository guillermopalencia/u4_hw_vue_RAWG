<template>
  <div class="card">
    <div class="image-wrapper">
      <img :src="image"/>
    </div>
    <div class="info-wrapper flex-col">
      <h1>{{ name }}</h1>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'GenreCard',
    props: ['name', 'image']
  }
</script>
