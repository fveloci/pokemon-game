<template>
    <div class="pokemon-container">
        <img 
            :src='imgSrc'
            v-if="!showPokemon"
            class="hidden-pokemon"
            alt="pokemon">
        <img
            v-else 
            class="fade-in" 
            :src='imgSrc' 
            alt="pokemon">
    </div>
  
</template>

<script>
export default {
    props: { 
        pokemonId: {type: Number, required: true},
        showPokemon: {type: Boolean, required: true, default: false}
    },
    computed: {
        imgSrc() {
            return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`
        }
    }
}
</script>

<style scoped>
/* Pokemon Picture */
.pokemon-container {
    height: 200px;
    width: auto;
    display: flex;
    justify-content: center;
    align-items: center;
}
img {
    width: 100vw;
    height: 200px;
    user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    -webkit-user-drag: none;
    -webkit-user-select: none;
}
.hidden-pokemon {
    filter: brightness(0);
}

</style>