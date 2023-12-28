<template>
  
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(pokemon, index) in pokemons" :key="index">
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
      pokemons: []
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

      this.pokemons = response.data.results

    });

  }

}
</script>

<style>

</style>
