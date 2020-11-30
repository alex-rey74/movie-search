<template>
  <div class="detail">
      <h1>{{this.title}}</h1>
      <img :src="'https://image.tmdb.org/t/p/w500/' + this.img">
      <p>Description : {{this.description}}</p>
      <ul>
          <li v-for="genre in this.genre" :key="genre">{{genre.name}}</li>
      </ul>
  </div>
</template>

<script>
/* eslint-disable no-console */
export default {
  name: 'Detail',
  data(){
      return {
          title: '',
          img: '',
          description: '',
          genre: []
      }
  },
  mounted(){
      const movieId = '/' + this.$route.params.movieId;

      let baseUrl = 'https://api.themoviedb.org/3/';
      let apiKey = '?api_key=723e373c4a4c78a28ed30f147409118b';

      let search = baseUrl + 'movie' + movieId + apiKey + '&query=' + this.query + '&include_adult=false'

      fetch(search)
      .then(rawJson => rawJson.json())
      .then(result => {
        this.title = result.title
        this.img = result.poster_path
        this.description = result.overview
        this.genre = result.genres
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
