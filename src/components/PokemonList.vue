<template>
  <div class="pokemon-layout">
    <div v-for="pokemon in filteredPokemons" :key="pokemon.name" class="pokemon-card">
      <div class="imagen">
        <img :src="pokemon.img" :alt="`Imagen de ${pokemon.name}`" />
      </div>
      <h3 class="nombre">{{ pokemon.name }}</h3>
      <p><b class="id">ID:</b> {{ pokemon.id }}</p>
      <p><b class="tipo">Tipo: </b>{{ pokemon.types.join(', ') }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    pokemons: {
      type: Array,
      required: true
    },
    filteredPokemons: {
      type: Array,
      required: true
    }
  }
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
  width: 400px;
  height: 350px;
  border-radius: 10px;
  color: #000;
}
.imagen {
  background-color: #000;
  border-radius: 10px;
}
img {
  background-color: #000;
  width: 200px;
  height: 150px;
}
.nombre {
  color: #ffcb05;
  text-shadow: -1px -1px 0 #007acc, 1px -1px 0 #007acc, -1px 1px 0 #007acc, 1px 1px 0 #007acc;
}
</style>
