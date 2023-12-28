<template>
  
  <div>

    <div class="card" style="display: flex; align-items: center; flex-direction: column">

        <div class="card-content">
            <div class="media">
                <div class="media-content">
                    <p class="title is-4">{{ num }} - {{ capitalizeName }}</p>
                    <p class="subtitle is-6">{{ pokemon.type }}</p>
                </div>
            </div>

            <div class="content">
            </div>

        </div>

        <div class="card-image">
            <figure>
                <img :src="currentImg" alt="Placeholder image">
            </figure>
        </div>

        <button class="button is-half" @click="mudarSprite">Mudar sprite</button>

    </div>

  </div>

</template>

<script>
import axios from "axios";
import _ from "lodash";

export default {

    created: function(){

        axios.get(this.url).then((response) => {
            this.pokemon.type = response.data.types[0].type.name
            this.pokemon.front = response.data.sprites.front_default
            this.pokemon.back = response.data.sprites.back_default

            this.currentImg = this.pokemon.front;
        });

    },

    data(){
        return {
            isFront: true,
            currentImg: "",
            pokemon: {}
        }
    },

    props: {
        num: Number,
        name: String,
        url: String
    },

    computed: {
        capitalizeName(){
            return _.upperFirst(this.name);
        }
    },

    methods: {
        mudarSprite(){
            if(this.isFront){
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            }else{
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }

}
</script>

<style>
    .card{
        margin-top: 2%;
    }

    .button{
        margin-bottom: 16px;
    }
</style>