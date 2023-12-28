<template>
  
  <div>Olá, mundo!</div>


</template>

<script>

import axios from "axios";

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

  created: function(){

    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(response => {

      console.log("Requisição dos pokemons da primeira geração")

      this.pokemons = response.data.results

    });

  }

}
</script>

<style>

</style>
