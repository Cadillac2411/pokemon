<template>
  <v-carousel  hide-delimiters show-arrows="hover" height="100%" hide-delimiter-background>
    <v-carousel-item v-for="(imagen, index) in imagenesPokemons" :key="index">
      <v-img :src="imagen" aspect-ratio="1"></v-img>
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
.v-carousel {
  width: 100%;
  height: 100%;
}


</style>
