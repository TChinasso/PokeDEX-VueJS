<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <input class="input is-hovered" id="busca" type="text" placeholder="Buscar Pokemon" v-model="busca">
      <button class="button is-success" @click="buscaPoke">Buscar</button>
      <div v-for="(poke,index) in filteredPokemons" :key="poke.name">
        <Pokemon :index="index + 1" :name="poke.name" :url="poke.url"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  data (){
    return{
      busca: "",
      pokemons: [],
      filteredPokemons: []
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(response => {
      this.pokemons = response.data.results;
      this.filteredPokemons = response.data.results;
    })
  },
  components: {
    Pokemon
  },
  computed: {
    // resultadoBusca: function() {
    //   if(this.busca == '' || this.busca == ' '){
    //     return this.pokemons
    //   } else {
    //     return this.pokemons.filter(pokemon => pokemon.name == this.busca)
    //   }
    // }

  },
  methods: {
    buscaPoke: function(){
      this.filteredPokemons = this.pokemons
      if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons
      } else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca.toLowerCase())
      }
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
#busca{
  width: 80%;
  margin-right: 20px;
  display: inline;
}
</style>
