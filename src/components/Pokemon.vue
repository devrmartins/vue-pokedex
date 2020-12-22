<template>
  <div class="pokemon">
    <h4>{{ num }} {{ name | upper }}</h4>
    <p>{{ url }}</p>
  </div>
</template>
<script>
export default {
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
<style scoped></style>
