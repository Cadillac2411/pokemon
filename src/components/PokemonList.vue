<template>
  <div class="pokemon-layout">
    <div v-for="pokemon in filteredPokemons" :key="pokemon.name" class="pokemon-card">
      <div class="imagen">
        <PokemonCarousel :imagenesPokemons="pokemon.imagenesPokemons" />
      </div>
      <h3 class="nombre">{{ pokemon.name }}</h3>
      <p><b class="id">ID:</b> {{ pokemon.id }}</p>
      <p><b class="tipo">Tipo: </b>{{ pokemon.types.join(', ') }}</p>
      <PokemonStats :pokemon="pokemon" />
    </div>
  </div>
</template>

<script>
  import PokemonCarousel from '/src/components/PokemonCarousel.vue';
  import PokemonStats from '/src/components/PokemonStats.vue';
  export default {
    components: {
      PokemonStats,
      PokemonCarousel,
    },
    props: {
      pokemons: {
        type: Array,
        required: true,
      },
      filteredPokemons: {
        type: Array,
        required: true,
      },
    },
  };
</script>

<style>
  .pokemon-layout {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }
  .pokemon-card {
    border: 2px solid #ffcb05;
    padding: 20px;
    margin: 10px;
    width: 200px;
    border-radius: 10px;
    color: #000;
    text-align: center;
    /* Agregar sombreado al borde */
    box-shadow: 0 3px 10px rgba(0, 0, 1, 1);
  }

  .imagen {
    border-radius: 10px;
  }

  img {
    background-image: url('https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRC7zBdc82XiS1wIVmKLgjC9JrbaFZomzP2Iiapce6_5g&s');
    border-radius:30px;
  }

  .nombre {
    color: #ffcb05;
    text-shadow: -1px -1px 0 #007acc, 1px -1px 0 #007acc, -1px 1px 0 #007acc, 1px 1px 0 #007acc;
    font-size: 24px;
  }
</style>
