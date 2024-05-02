<template>
  <div class="pokemon-layout">
    <div v-for="pokemon in filteredPokemons" :key="pokemon.name" class="pokemon-card">
      <div class="imagen">
        <img :src="pokemon.img" :alt="`Imagen de ${pokemon.name}`" />
      </div>
      <h3 class="nombre">{{ pokemon.name }}</h3>
      <p><b class="id">ID:</b> {{ pokemon.id }}</p>
      <p><b class="tipo">Tipo: </b>{{ pokemon.types.join(', ') }}</p>
      <v-dialog max-width="500">
  <template v-slot:activator="{ props: activatorProps }">
    <v-btn
      v-bind="activatorProps"
      color="surface-variant"
      text="Open Dialog"
      variant="flat"
    ></v-btn>
  </template>

  <template v-slot:default="{ isActive }">
    <v-card title="Dialog">
      <v-card-text>
        Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
      </v-card-text>

      <v-card-actions>
        <v-spacer></v-spacer>

        <v-btn
          text="Close Dialog"
          @click="isActive.value = false"
        ></v-btn>
      </v-card-actions>
    </v-card>
  </template>
</v-dialog>
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
        width: 200px;
        border-radius: 10px;
        color: #000;
        text-align: center;
    }
.imagen {
  background-color: #000;
  border-radius: 10px;
}
img {
  background-color: #000;
}
.nombre {
  color: #ffcb05;
  text-shadow: -1px -1px 0 #007acc, 1px -1px 0 #007acc, -1px 1px 0 #007acc, 1px 1px 0 #007acc;
}
</style>
