<template>
  
  <div>
    <h1>{{ num }} - {{ capitalizeName }}</h1>
    <small>{{ url }}</small>
    <hr>
  </div>

</template>

<script>
import _ from "lodash";

export default {

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

}
</script>

<style>

</style>