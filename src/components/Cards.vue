<template>
    <div>
        <!-- img src is determined by computed property -->
        <img :src="getImageSrc" style="width:10%">
        <h2 v-if="pokeName"> {{ pokeName }}</h2>
        <b v-if="pokeType">Type(s): {{type1}} <b v-if="type2">,</b> {{type2}} </b>
        <br/>
        <b v-if="pokeId"> {{pokeId}} </b>
    </div>
</template>

<script>

export default {
    name: 'Cards',
    props: [
        "pokeId",
        "pokeName",
        "pokeType"
    ],

    data() {
        return {
            name: null,
            id: null,
            type1: null,
            type2: null,
        }
    },

    computed:{
        getImageSrc(){
            return `https://pokeres.bastionbot.org/images/pokemon/${this.pokeId}.png`
        }
    },

    methods: {
        processTypes(){
            if (this.pokeType[0]){
                this.type1 = this.pokeType[0]["type"]["name"]
            }
            if (this.pokeType[1]){
                this.type2 = this.pokeType[1]["type"]["name"]
            } else {
                this.type2 = null;
            }
        }
    },
    updated: function(){
        this.$nextTick( function() {
            this.processTypes()
        })
    }
}


</script>


