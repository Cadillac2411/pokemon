<template>
  <v-carousel hide-delimiters show-arrows="hover" height="100%" hide-delimiter-background class="custom-carousel">
    <v-carousel-item v-for="(imagen, index) in imagenesPokemons" :key="index">
      <v-img :src="imagen" aspect-ratio="1" class="carousel-image"></v-img>
    </v-carousel-item>
  </v-carousel>
</template>

<script>
export default {
  props: {
    imagenesPokemons: {
      type: Array,
      required: true
    }
  }
};
</script>

<style scoped>

</style>
