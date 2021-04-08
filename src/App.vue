<template>
  <div id="app">
     <img width="600px" height="200px" src="./assets/pokemon-png-logo.png">

      <div class="column is-half is-offset-one-quarter">
            <hr>
            <h4 class="is-size-4">Pokedex</h4>
            <input  type="text" id="" placeholder="Buscar pokemon" v-model="busca"/>
            <button @click="buscar">Buscar</button>
            <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
                <Pokemon :name="poke.name" :url="poke.url" :num="index + 1"/>
            </div>
      </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';

export default {
  name: 'App',
  data(){
    return{
        pokemons: [],
        filteredPokemons: [],
        busca: ''
    }
  },
  created: function(){
  axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
        console.log("Pegou a lista de pokemons")
        this.pokemons = res.data.results
        this.filteredPokemons = res.data.results
  })

},
  components:{
    Pokemon
  },
  methods: {
    buscar: function(){
        this.filteredPokemons = this.pokemons;
      if(this.busca == '' || this.busca == ''){
        this.filteredPokemons = this.pokemons
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    }
  },
  computed: {
    /*
    resultadoBusca: function(){
      if(this.busca == '' || this.busca == '')
        return this.pokemons;
      else
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
    }
    */
  }
 
}
</script>

<style>
  #app{
    display:flex;
    flex-direction: column;
    align-items:center;
    justify-content: center;
  }
</style>
