<template>
    <div>
        <!-- custom event comes from SearchBar.vue fetch method -->
        <search-bar
            @search-click-event="returnPokemonData"
        ></search-bar>
        <card-container
            :pokeData="this.pokemonData"
        ></card-container>
    </div>
</template>

<script>
import SearchBar from './SearchBar.vue'
import CardContainer from './CardContainer.vue'

export default {
    name: 'MainContainer',
    components: {
        SearchBar,
        CardContainer
    },
    data() {
        return {
            pokemonData: 'None'
        }
    },
    methods: {
        returnPokemonData(pokemon_json){
            console.log(pokemon_json)
            this.pokemonData = pokemon_json;
            // alert("this works")
        }
    },
}


</script>

