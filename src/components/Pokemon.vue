<template>
  <div id="pokemon" class="card">
    <div class="card-image">
      <figure class="image is-128x128">
        <img :src="pokemon.sprites.front_default" alt="Placeholder image" />
      </figure>
    </div>
    <div class="card-content">
      <div class="media-content">
        <p class="title is-4 mb-3">{{ this.name }}</p>
        <ul class="types">
          <li class="type" v-for="(t, index) of pokemon.types" :key="index">
            {{ t.type.name }}
          </li>
        </ul>
      </div>
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
#pokemon .image {
  margin: 0 auto;
}
.types {
  display: flex;
}
.types .type {
  background-color: rgb(236, 236, 236);
  padding: 5px 15px;
  margin-right: 5px;
  border-radius: 15px;
}
</style>
