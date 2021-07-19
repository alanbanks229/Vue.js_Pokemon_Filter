<template>
    <div>
        <p v-if="pokeData === 'None' "> NO DATA </p>
            <!-- v-for="card in pokeData" -->
        <cards
            :pokeName="pokeData.name"
            :pokeId="pokeData.id"
            :pokeType="pokeData.types"
        ></cards>
    </div>
</template>

<script>
import Cards from './Cards.vue'

export default {
    name: 'CardContainer',
    // remember props represent what a child component is receiving from parent
    props: [
        "pokeData"
    ],
    components: {
        Cards,
    },


    data(){
        return {
            errorMsg: "",
        }
    },
}


</script>

