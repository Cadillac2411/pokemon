<template>
  <v-dialog max-width="1000">
    <template v-slot:activator="{ props: activatorProps }">
      <v-btn
        class="boton"
        v-bind="activatorProps"
        color="#ffcd0568"
        border-color="yellow"
        text="Estadísticas"
        variant="flat"
        large></v-btn>
    </template>

    <template v-slot:default="{ isActive }">
      <v-card :title="`Estadísticas de ${pokemon.name}`">
        <v-card-text class="textoEstadisticas">
          <ul class="lista">
            <li>
              <p class="estadisticaTexto">
                <img
                  class="iconoEstadistica"
                  src="https://static.vecteezy.com/system/resources/previews/002/513/330/non_2x/red-heart-pixel-art-vector.jpg"
                  alt="" /><strong>Salud:</strong> {{ pokemon.salud }}
              </p>
            </li>
            <li class="ajusteLista">
              <p class="estadisticaTexto">
                <img
                  class="iconoEstadistica"
                  src="https://img.freepik.com/vector-premium/elemento-juego-sword-pixel-art-espada-pixeles-juego_158677-574.jpg?w=2000"
                  alt="" /><strong>Ataque:</strong> {{ pokemon.ataque }}
              </p>
            </li>
            <li class="ajusteLista">
              <p class="estadisticaTexto">
                <img
                  class="iconoEstadistica"
                  src="https://th.bing.com/th/id/OIP.RpRHxFg1xGutPwZNeM_qMAHaHa?rs=1&pid=ImgDetMain"
                  alt="" /><strong>Defensa:</strong> {{ pokemon.defensa }}
              </p>
            </li>
            <li class="ajusteLista">
              <p class="estadisticaTexto">
                <img
                  class="iconoEstadistica"
                  src="https://static.vecteezy.com/system/resources/previews/010/826/102/original/lightning-pixel-art-free-vector.jpg"
                  alt="" /><strong>Velocidad:</strong> {{ pokemon.velocidad }}
              </p>
            </li>
          </ul>

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
  v-btn {
    margin-top: 1rem;
  }
  .boton {
    color: yellow;
    background-color: white;
    border-radius: 2px;
  }
  .textoEstadisticas {
    font-family: 'Times New Roman', Times, serif;
  }

  .estadisticaTexto {
    font-size: 30px;
    margin-left: 2.5rem;
  }

  v-card .title {
    font-size: 60px;
  }

  .iconoEstadistica {
    height: 35px;
    width: 40px;
  }

  .lista {
    display: flex;
  }

  li {
    list-style: none;
  }


</style>
