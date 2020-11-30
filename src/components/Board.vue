<template>
  <div class="board">
      <ul class="list-group">
          <li class="list-group-item" v-for="movie in movies" :key="movie.id">
              {{movie.title}}
              <button class="btn btn-danger" @click="deleteCallback(movie.id)">Delete</button>
            </li>
      </ul>
      
  </div>
</template>

<script>
export default {
  name: 'Board',
  props: {
      movies: Array,
      deleteCallback: Function,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
