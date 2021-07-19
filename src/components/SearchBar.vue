<template>
    <div>
            <label for="poke_name">Enter a pokemon name</label>
            <br/>
            <input @keyup.enter="getSpecificPokemon" name="poke_name" type="text" ref="search_query">
            <br/>
            <button @click="getSpecificPokemon">Search</button>
    </div>
</template>

<script>

export default {
    name: 'SearchBar',

    methods: {
        // child communication with parent (MainContainer)

        getSpecificPokemon(){
            console.log(this.$refs)
            fetch("https://pokeapi.co/api/v2/pokemon/" + this.$refs.search_query.value)
                .then(response => response.json())
                .then(data => {
                    this.$emit('search-click-event', data);
                })
            .catch(error => {
                this.errorMsg = error;
                console.log(error)
            })
        }

    }
}


</script>

<style>
button{
    margin: 1rem;
    padding: 1rem;
}
</style>