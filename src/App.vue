<template>
  
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
    
    <h1 class="is-size-4">Pokedex</h1>
    <div style="display: flex;">
      <input class="input is-rounded" type="text" placeholder="Buscar pelo nome" v-model="busca">
      <button class="button is-half is-rounded is-success" @click="buscar">Buscar</button>
   
    </div>

      <div v-for="(pokemon, index) in filteredPokemons" :key="pokemon.url">
        <pokemonComponent :name="pokemon.name" :url="pokemon.url" :num="index + 1"/>
      </div>

    </div>

  </div>

</template>

<script>

import axios from "axios";
import pokemonComponent from "./components/pokemonComponent.vue"

export default {
  name: 'App',

  data(){

    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }

  },

  mounted() {
    document.title = 'Pokedex com Vue.js'
  },

  components: {
    
    pokemonComponent,

  },

  created: function(){

    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(response => {

      this.pokemons = response.data.results;
      this.filteredPokemons = response.data.results

    });

  },

  methods: {

    buscar: function(){

      this.filteredPokemons = this.pokemons;

      if(this.busca == '' || this.busca == '  '){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }

    }

  },

  computed: {

    // resultadoBusca: function(){

    //   if(this.busca == '' || this.busca == '  '){
    //     return this.pokemons;
    //   }else{
    //     return this.pokemons.filter(pokemon => pokemon.name == this.busca)
    //   }

    // }

  }

}
</script>

<style>
  h1{
    margin-top: 16px !important;
    margin-bottom: 8px !important;
  }

  input{
    margin-right: 16px !important;
  }
</style>
