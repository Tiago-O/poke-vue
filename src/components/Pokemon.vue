<template>

  <h1>Pokémon</h1>

  <div>
    name:
    {{ pokemon.name }}
  </div>

  <div>
    hp:
    {{ pokemon.stats[0].base_stat }}
  </div>

  <div>
    <img :src="pokemon.sprites.front_default" alt="">
  </div>

  <h4>types:</h4>
  <ul v-for="t in pokemon.types">
    <li>{{t.type.name}}</li>
  </ul>

  <button @click="newPokemon">New Pokemon!</button>

</template>

<script>
import axios from "axios";

export default {
  name: "Pokemon",

  data() {
    return {
      pokemon: [],
      errors: []
    }
  },

  created() {
    let r = Math.floor(Math.random() * 898) + 1;
    axios.get(`https://pokeapi.co/api/v2/pokemon/` + r)
        .then(response => {
          this.pokemon = response.data
        })
        .catch(e => {
          this.errors.push(e)
        })
  },

  methods: {
    newPokemon(event) {
      let r = Math.floor(Math.random() * 898) + 1;
      axios.get(`https://pokeapi.co/api/v2/pokemon/` + r)
          .then(response => {
            this.pokemon = response.data
          })
          .catch(e => {
            this.errors.push(e)
          })
    }

  }
}
</script>

<style scoped>


</style>