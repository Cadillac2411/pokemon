<template>
    <div>
      <h1 class="titulo">Pokémon</h1>
      <div class="filtro">
        <input v-model="searchTerm" placeholder="Buscar por nombre o ID" />
        <div class="pokemon-layout">
          <div
            v-for="pokemon in filteredPokemons"
            :key="pokemon.name"
            class="pokemon-card"
          >
            <div class="imagen">
              <img :src="pokemon.img" :alt="`Imagen de ${pokemon.name}`" />
            </div>
            <h3 class="nombre">{{ pokemon.name }}</h3>
            <p><b class="id">ID:</b> {{ pokemon.id }}</p>
            <p><b class="tipo">Tipo: </b>{{ pokemon.types.join(", ") }}</p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  
  export default {
    data() {
      return {
        pokemons: [],
        searchTerm: "",
      };
    },
    computed: {
      filteredPokemons() {
        return this.pokemons.filter(pokemon =>
        pokemon.id === parseInt(this.searchTerm)||
        pokemon.name.toLowerCase().includes(this.searchTerm.toLowerCase())
      )},
    },
    created() {
      this.fetchAllPokemons();
    },
    methods: {
      async fetchAllPokemons() {
        try {
          const response = await axios.get(
            "https://pokeapi.co/api/v2/pokemon/?limit=811"
          );
          const pokemonList = response.data.results;
          await Promise.all(
            pokemonList.map(async (pokemon) => {
              const pokemonResponse = await axios.get(pokemon.url);
              this.pokemons.push({
                name: this.capitalizarPrimeraLetra(pokemonResponse.data.name),
                id: pokemonResponse.data.id,
                types: pokemonResponse.data.types.map(
                  (typeInfo) => typeInfo.type.name
                ),
                img: pokemonResponse.data.sprites.front_default,
              });
            })
          );
          // Ordenar los Pokémon por ID de menor a mayor
          this.pokemons.sort((a, b) => a.id - b.id);
        } catch (error) {
          console.error("Error fetching Pokémon data:", error);
        }
      },
      capitalizarPrimeraLetra(string) {
        return string.charAt(0).toUpperCase() + string.slice(1);
      },
    },
  };
  </script>
  
  

<style>
  * {
    background-color: white;
  }

  input {
    text-align: center;
  }

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
  }

  .imagen {
    background-color: #000;
    border-radius: 10px;
  }
  img {
    background-color: #000;
  }

  .titulo {
    color: #ffcb05;
    text-shadow: -1px -1px 0 #007acc, 1px -1px 0 #007acc, -1px 1px 0 #007acc,
      1px 1px 0 #007acc;
    text-align: center;
  }

  .nombre {
    color: #ffcb05;
    text-shadow: -1px -1px 0 #007acc, 1px -1px 0 #007acc, -1px 1px 0 #007acc,
      1px 1px 0 #007acc;
  }

  .filtro {
    color: #000;
    text-align: center;
    font-family: "Times New Roman", Times, serif;
  }
</style>

<!-- Las directivas de Vue son atributos especiales con el prefijo v- que puedes agregar a cualquier elemento HTML en tus plantillas de Vue. Estas directivas te permiten realizar tareas dinámicas directamente en el DOM, como manipular el texto, enlazar datos, manejar eventos y realizar muchas otras acciones que serían más complejas de hacer con JavaScript puro.

Aquí hay algunas de las directivas más comunes y su uso:

v-model: Crea un enlace bidireccional en formularios o componentes, permitiendo que el estado de la aplicación y los campos de entrada estén sincronizados.
v-for: Utilizado para renderizar una lista de elementos basándose en los datos de un arreglo.
v-if, v-else-if, v-else: Directivas condicionales que sirven para incluir o excluir elementos del DOM basándose en alguna condición.
v-show: Similar a v-if, pero en lugar de eliminar elementos, simplemente alterna su visibilidad con CSS.
v-bind: Enlaza atributos HTML a expresiones de Vue. Por ejemplo, puedes enlazar el atributo href de un enlace a una variable en tu instancia de Vue.
v-on: Escucha eventos del DOM y ejecuta JavaScript cuando estos ocurren. Es útil para manejar eventos como clics, entradas de teclado, etc.
Cada directiva puede tener argumentos y modificadores que alteran su comportamiento. Por ejemplo, v-on:click.prevent escuchará el evento de clic y llamará a event.preventDefault() automáticamente.

Las directivas son una parte fundamental de Vue que facilita la creación de interfaces de usuario reactivas y dinámicas -->

<!-- Axios es un cliente HTTP basado en promesas para Node.js y el navegador. Es isomórfico, lo que significa que puede ejecutarse tanto en el navegador como en Node.js con la misma base de código. En el lado del servidor, utiliza el módulo http nativo de Node.js, mientras que en el cliente (navegador) utiliza XMLHttpRequests.

Algunas características de Axios incluyen:

Realizar solicitudes XMLHttpRequests desde el navegador.
Realizar solicitudes HTTP desde Node.js.
Soportar la API de promesas.
Interceptar peticiones y respuestas.
Transformar datos de peticiones y respuestas.
Cancelar peticiones.
Configurar tiempos de espera (timeouts).
Serializar parámetros de consulta.
Automatizar la serialización del cuerpo de la solicitud a JSON, formularios multipartes y URL codificadas.
Manejar automáticamente los datos JSON en la respuesta.
Axios es ampliamente utilizado debido a su interfaz fácil de usar y su capacidad para manejar peticiones y respuestas de manera eficiente -->
