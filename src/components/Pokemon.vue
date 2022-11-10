<template>

  <div class="card">

    <img :src="pokemon.sprites.front_default" alt="">

    <div class="info">
      <p>
        Name:
        {{pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1)}}
      </p>

      <p>
        HP:
        {{ pokemon.stats[0].base_stat }}
      </p>

      <p>Types:</p>
      <ul v-for="t in pokemon.types">
        <li>
          {{t.type.name.charAt(0).toUpperCase() + t.type.name.slice(1)}}
        </li>
      </ul>
    </div>

    <button @click="newPokemon">New Pokemon!</button>

  </div>



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

.card {
  border: solid #2ea44f 2px;
  border-radius: 12px;
  width: 200px;
}

img {
  margin: auto;
  display: block;
  padding: 16px;
}

.info {
  margin: auto;
  display: block;
  padding: 0 20px;
}

p, li {
  font-weight: 500;
  color: black;
}

ul{
  list-style-type:none;
}

button {
  margin: 20px auto 20px auto;
  display: block;
  width: 160px;
  background-color: #2ea44f;
  color: #fff;
  border: 1px solid rgba(27, 31, 35, .15);
  border-radius: 6px;
  box-shadow: rgba(27, 31, 35, .1) 0 1px 0;
  box-sizing: border-box;
  cursor: pointer;
  font-weight: bold;
  line-height: 20px;
  padding: 8px;
  white-space: nowrap;
}

</style>