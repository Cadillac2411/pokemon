<template>
  <v-dialog max-width="500">
    <template v-slot:activator="{ props: activatorProps }">
      <v-btn class="boton" v-bind="activatorProps" color="#ffcd0568" border-color="yellow" text="Estadísticas" variant="flat"></v-btn>
    </template>

    <template v-slot:default="{ isActive }">
      <v-card :title="`Estadísticas de ${pokemon.name}`">
        <v-card-text class="textoEstadisticas">
          <p><strong>Salud:</strong> {{ pokemon.salud }}</p>
          <p><strong>Ataque:</strong> {{ pokemon.ataque }}</p>
          <p><strong>Defensa:</strong> {{ pokemon.defensa }}</p>
          <p><strong>Velocidad:</strong> {{ pokemon.velocidad }}</p>
          <!-- ... otras estadísticas ... -->
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
export default {
  props: {
    pokemon: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style>
.boton {
  color: yellow;
  background-color: white;
}
.textoEstadisticas {
  font-family: 'Times New Roman', Times, serif;
}
</style>
