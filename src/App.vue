<template>
  <div id="app" class="container">
    <div id="pokemons" class="columns is-multiline">
      <div
        class="column is-3"
        v-for="(pokemon, index) in pokemons"
        :key="index"
      >
        <Pokemon :name="pokemon.name" :url="pokemon.url" />
      </div>
    </div>
  </div>
</template>

<script>
import api from "./api";
import Pokemon from "./components/Pokemon";

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
  color: #2c3e50;
  margin-top: 15px;
  margin-bottom: 15px;
}
</style>
