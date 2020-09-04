<template>
  <div id="app">
    <h1>Omdb Website Using Vue</h1>

    <div>
      <input type='text' placeholder="Enter Your Movie" v-model='searchTerm'>
      <button v-on:click='search'>Search</button>
    </div>

    <div>
      <h2>Result:</h2>

      <div id='movie-list' v-for="film in films" :key="film.imdbID" v-on:click='selectFilm(film)'>
      <img v-bind:src='film.Poster'>
      <h3>{{film.Title}}</h3>
      <p>{{film.Year}} - {{film.Type}}</p>
      </div>

    </div>

    <div id='movie-info' v-if='selectedFilm'>
      <h4>{{selectedFilm.Title}}</h4>
      <p>{{selectedFilm.Year}}</p>
      <p>{{selectedFilm.Genre}}</p>
      <p>{{selectedFilm.Director}}</p>
      <p>{{selectedFilm.Writer}}</p>
      <p>{{selectedFilm.Actors}}</p>

      <h5>{{selectedFilm.Plot}}</h5>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',

  methods: {
    search: function(){
      fetch('http://www.omdbapi.com/?s='+this.searchTerm+'&apikey=87d10179').then(response => response.json()).then(data => this.films = data.Search);
    },

    selectFilm: function(film){
      fetch('http://www.omdbapi.com/?i='+film.imdbID+'&apikey=87d10179').then(response => response.json()).then(this.selectedFilm = film);
    }
  },

  data(){
    return{
      searchTerm: '',
      selectedFilm: null,
      films:[]
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
