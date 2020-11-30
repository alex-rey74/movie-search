<template>
<div class="container-search">
    <div class="search">
        <input class="form-control input-search" type="text" v-model="query">
        <button @click="onQuery" class="btn btn-primary btn-search">Valider</button>
        <ul class="list-group">
            <li class="list-group-item" v-for="content in topRated" :key="content.id" @click="onMovieClick(content)">
                <p>{{content.title}}</p>
            </li>
        </ul>
  </div>
  <div class="list">
      <board :movies="this.selectedMovies" :deleteCallback="deleteMovie"></board>
  </div>
</div>

</template>

<script>
/* eslint-disable no-console */
import Board from '@/components/Board'

export default {
  name: 'Search',
  components:{
      Board
  },
  data(){
    return {
      topRated: [],
      selectedMovies: [],
      query: ''
    }
  },
  mounted(){
  },
  methods : {
    deleteMovie(movieId){
        this.selectedMovies = this.selectedMovies.filter(movie => {
            return movie.id !== movieId
        })

        /*
        this.selectedMovies.forEach((item, index) => {
            if(item.id === id){
                this.selectedMovies.splice(index, 1)
            }
        })
        */
    },
    onMovieClick(content){
        this.selectedMovies.push(content);
        window.localStorage.setItem('movies', JSON.stringify(this.selectedMovies))
    },
    onQuery(){
      let baseUrl = 'https://api.themoviedb.org/3/';
      let apiKey = '?api_key=723e373c4a4c78a28ed30f147409118b';

      let search = baseUrl + 'search/movie' + apiKey + '&query=' + this.query + '&include_adult=false'

      fetch(search)
      .then(rawJson => rawJson.json())
      .then(result => {
        this.topRated = result.results;
    })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container-search{
    display: flex;
}
.search{
    height: 100vh;
    width: 20rem;
    overflow: auto;
}

.btn-search{
    margin: 10px;
}

.list{
    width:100%;
}
</style>
