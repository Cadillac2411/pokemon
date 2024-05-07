<template>
    <v-dialog max-width="500">
      <template v-slot:activator="{ props: activatorProps }">
        <v-btn v-bind="activatorProps" color="surface-variant" text="Estadísticas" variant="flat"></v-btn>
      </template>
  
      <template v-slot:default="{ isActive }">
        <v-card :title="`Estadísticas de ${pokemon.name}`">
          <v-card-text>
            <p>Ataque: {{ pokemon.ataque }}</p>
            <p>Defensa: {{ pokemon.defensa }}</p>
            <p>Velocidad: {{ pokemon.velocidad }}</p>
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
  