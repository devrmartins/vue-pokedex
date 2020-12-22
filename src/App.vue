<template>
  <div id="app">
    <div class="pokemons">
      <Pokemon
        v-for="(pokemon, index) in pokemons"
        :key="index"
        :name="pokemon.name"
        :url="pokemon.url"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";

const api = axios.create({
  baseURL: "https://pokeapi.co/api/v2",
});
export default {
  name: "App",
  components: {
    Pokemon,
  },
  data() {
    return {
      pokemons: [],
    };
  },
  created: async function() {
    let params = new URLSearchParams();
    params.append("limit", 151);
    params.append("offset", 0);

    let res = await api.get(`/pokemon?${params.toString()}`);
    this.pokemons = res.data.results;
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
