<template>
  <div id="pokemon">
    <div class="card">
      <div class="card-image">
        <figure
          v-if="currentImg"
          class="image is-128x128"
          @mouseenter="changeSprite('back')"
          @mouseleave="changeSprite('front')"
        >
          <img :src="currentImg" alt="Placeholder image" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
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
    </div>
  </div>
</template>
<script>
import api from "../api";
export default {
  async created() {
    this.isFront = true;
    let pokemon = await api.get(this.url);
    this.pokemon = pokemon.data;
    this.currentImg = this.pokemon.sprites.front_default || "";
  },
  data() {
    return {
      isFront: Boolean,
      currentImg: String,
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
  methods: {
    changeSprite(current) {
      if (current == "back") {
        this.isFront = false;
        this.currentImg = this.pokemon.sprites.back_default;
      } else {
        this.isFront = true;
        this.currentImg = this.pokemon.sprites.front_default;
      }
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
