<template>
  <div id="app">    
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/pokemon.png" alt="12%">
      <h1 class="is-size-3">Pokédex</h1>
      <div v-for="(poke, index) in pokemons" :key="index">
        <Pokemon :num="index + 1" :name="poke.name" :url="poke.url" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon.vue";

export default {
  name: "App",

  data() {
    return {
      pokemons: [],
    };
  },

  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        console.log("Pegou a lista de pokemons");
        this.pokemons = res.data.results;
      });
  },

  components: {
    Pokemon,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
