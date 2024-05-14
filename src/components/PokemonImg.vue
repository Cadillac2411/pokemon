<template>
  <v-dialog max-width="1000">
    <template v-slot:activator="{ props: activatorProps }">
      <v-btn
        class="botonImg"
        v-bind="activatorProps"
        color="#ffcd0568"
        border-color="yellow"
        text="Imagenes"
        variant="flat"
        large></v-btn>
    </template>

    <template v-slot:default="{ isActive }">
      <v-card :title="`Imagenes de ${pokemon.name}`">
        <v-card-text class="carruselImg">
          <PokemonCarousel :imagenesPokemons="pokemon.imagenesPokemons" />
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn text="Cerrar" @click="isActive.value = false"></v-btn>
        </v-card-actions>
      </v-card>
    </template>
  </v-dialog>
</template>

<script>
  import PokemonCarousel from '/src/components/PokemonCarousel.vue';
  export default {
    components: {
      PokemonCarousel,
    },
    props: {
      pokemon: {
        type: Object,
        required: true,
      },
    },
  };
</script>

<style>
  .botonImg {
    color: yellow;
    background-color: white;
    border-radius: 2px;
    padding-left: 30px;
    padding-right: 30px;
    margin-left: 3px;
    text-align: center;
    margin-bottom: 14px;
  }

  v-card .title {
    font-size: 60px;
  }

  .carruselImg{
    width: 500px;
    height: 500px;
    margin-left: 250px;
  }
</style>
