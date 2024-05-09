<template>
  <div class="pokemon-layout">
    <div v-for="pokemon in paginatedPokemons" :key="pokemon.name" class="pokemon-card">
      <div class="imagen">
        <PokemonCarousel :imagenesPokemons="pokemon.imagenesPokemons" />
      </div>
      <h3 class="nombre">{{ pokemon.name }}</h3>
      <p class="id"><b>ID:</b> {{ pokemon.id }}</p>
      <p class="tipo"><b>Tipo: </b>{{ pokemon.types.join(', ') }}</p>
      <PokemonStats :pokemon="pokemon" />
    </div>
  </div>
  <div>
    <v-pagination v-model="currentPage" :length="totalPages" next-icon="mdi-chevron-right" prev-icon="mdi-chevron-left" class="custom-pagination">
      <template v-slot:prev-label> {{ currentPage }} / {{ totalPages }} </template>
      <template v-slot:next-label> {{ currentPage }} / {{ totalPages }} </template>
    </v-pagination>
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
    data() {
      return {
        currentPage: 1, // Página actual
        itemsPerPage: 10, // Cantidad de Pokémon por página
      };
    },
    computed: {
      totalPages() {
        return Math.ceil(this.filteredPokemons.length / this.itemsPerPage);
      },
      paginatedPokemons() {
        const startIndex = (this.currentPage - 1) * this.itemsPerPage;
        const endIndex = startIndex + this.itemsPerPage;
        return this.filteredPokemons.slice(startIndex, endIndex);
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
    border: 4px solid #ffcb05;
    padding: 20px;
    margin: 10px;
    width: 370px;
    height: 520px;
    border-radius: 10px;
    color: #000;
    text-align: center;
    /* Agregar sombreado al borde */
    box-shadow: 0 3px 15px rgba(0, 0, 1, 1);
  }

  .imagen {
    border-radius: 10px;
  }

  img {
    background-image: url('https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRC7zBdc82XiS1wIVmKLgjC9JrbaFZomzP2Iiapce6_5g&s');
    background-size: cover;
    border-radius: 10px;
  }

  .nombre {
    color: #ffcb05;
    text-shadow: -1px -1px 0 #007acc, 1px -1px 0 #007acc, -1px 1px 0 #007acc, 1px 1px 0 #007acc;
    font-size: 34px;
  }

  .id {
    font-size: 20px;
  }

  .tipo {
    font-size: 20px;
    padding-bottom: 9px;
  }

  .custom-pagination .v-pagination__item {
  color: #af8c00; /* Cambia el color a amarillo */
}
</style>
