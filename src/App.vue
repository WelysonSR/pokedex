<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/pokemon.png" alt="12%" />
      <h1 class="is-size-3">Pokédex</h1>
      <div class="control">
        <input
          class="input is-focused"
          type="text"
          placeholder="Buscar pokémon"
          v-model="busca"
        />
        <button
          class="button is-link is-outlined"
          id="buscaBtn"
          @click="buscar()"
        >
          Buscar
        </button>
      </div>
      <div v-for="(poke, index) in filteredpokemons" :key="poke.url">
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
      filteredpokemons: [],
      busca: "",
    };
  },

  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        console.log("Pegou a lista de pokemons");
        this.pokemons = res.data.results;
        this.filteredpokemons = res.data.results;
      });
  },

  components: {
    Pokemon,
  },

  methods: {
    buscar: function () {
       this.filteredpokemons = this.pokemons;
      if (this.busca == "" || this.busca == " ") {
        this.filteredpokemons = this.pokemons;
      } else {
        this.filteredpokemons = this.pokemons.filter((pokemon) => pokemon.name == this.busca);
      }
    },
  },

  computed: {
    /*resultadoBusca: function () {
      if (this.busca == "" || this.busca == " ") {
        return this.pokemons;
      } else {
        return this.pokemons.filter((pokemon) => pokemon.name == this.busca);
      }
    },*/
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
#buscaBtn {
  margin-top: 1.5%;
}
</style>
