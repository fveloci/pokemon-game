<template>
    <h1 v-if="!pokemon">Espere por favor...</h1>
    <div v-else>
      <h1>¿Quién es este pokemón?</h1>
      <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon"/>
      <PokemonOptions 
        :pokemons="pokemonArr"
        @selection="checkAnswer"
      />
      <template v-if="showAnswer">
        <h2>{{message}}</h2>
        <button @click="newGame">Nuevo Juego</button>
      </template>      
    </div>    
</template>

<script>
import PokemonOptions from '@/components/PokemonOptions.vue'
import PokemonPicture from '@/components/PokemonPicture.vue'
import getPokemonOptions from '@/helpers/getPokemonOptions'


export default {
  components: { PokemonOptions, PokemonPicture },
  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: ''
    }
  },
  methods: {
    async mixPokemonArray() {
      this.pokemonArr = await getPokemonOptions()
      const randomInt = Math.floor( Math.random() * 4 )
      this.pokemon = this.pokemonArr[randomInt]
    },
    checkAnswer(selectedId) {      
      this.showPokemon = true
      this.showAnswer = true
      if(selectedId === this.pokemon.id) {
        this.message = `Correcto, ${ this.pokemon.name }`
      } else {
        this.message = `Oops, era ${ this.pokemon.name }`
      }
    },
    newGame() {
      this.pokemon = null
      this.mixPokemonArray()
      this.showPokemon = false
      this.showAnswer = false
    }
  },
  mounted() {
    this.mixPokemonArray()
  }
}
</script>
