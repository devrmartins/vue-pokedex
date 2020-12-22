<template>
  <div id="pokemon" class="column is-3">
    <div class="box">
      <h4>{{ num }} {{ name | upper }}</h4>
      <ul class="types">
        <li class="type" v-for="(t, index) of pokemon.types" :key="index">
          {{ t.type.name }}
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import api from "../api";
export default {
  async created() {
    let pokemon = await api.get(this.url);
    this.pokemon = pokemon.data;
    console.log(pokemon);
  },
  data() {
    return {
      pokemon: Object,
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  filters: {
    upper: function(value) {
      return value.toUpperCase();
    },
  },
};
</script>
<style scoped>
.types {
  display: flex;
  padding: 5px 0;
}
.types .type {
  background-color: rgb(236, 236, 236);
  padding: 5px 15px;
  margin-right: 5px;
  border-radius: 15px;
}
</style>
