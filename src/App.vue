<template>
    <div>
        <h1 class="titulo">Pokémon</h1>
        <div class="filtro">
            <input v-model="searchTerm" placeholder="Buscar por nombre o ID" />
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
        </div>
    </div>
</template>

<script>
    import axios from 'axios';

    export default {
        data() {
            return {
                pokemons: [],
                searchTerm: '',
            };
        },
        computed: {
            filteredPokemons() {
                return this.pokemons.filter(
                    (pokemon) =>
                        pokemon.id === parseInt(this.searchTerm) ||
                        pokemon.name.toLowerCase().includes(this.searchTerm.toLowerCase())
                );
            },
        },
        created() {
            this.fetchAllPokemons();
        },
        methods: {
            async fetchAllPokemons() {
                try {
                    const response = await axios.get('https://pokeapi.co/api/v2/pokemon/?limit=811');
                    const pokemonList = response.data.results;
                    await Promise.all(
                        pokemonList.map(async (pokemon) => {
                            const pokemonResponse = await axios.get(pokemon.url);
                            this.pokemons.push({
                                name: this.capitalizarPrimeraLetra(pokemonResponse.data.name),
                                id: pokemonResponse.data.id,
                                types: pokemonResponse.data.types.map((typeInfo) => typeInfo.type.name),
                                img: pokemonResponse.data.sprites.front_default,
                            });
                        })
                    );
                    // Ordenar los Pokémon por ID de menor a mayor
                    this.pokemons.sort((a, b) => a.id - b.id);
                } catch (error) {
                    console.error('Error fetching Pokémon data:', error);
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

    .titulo {
        color: #ffcb05;
        text-shadow: -1px -1px 0 #007acc, 1px -1px 0 #007acc, -1px 1px 0 #007acc, 1px 1px 0 #007acc;
        text-align: center;
        font-size: 50px;
    }

    .nombre {
        color: #ffcb05;
        text-shadow: -1px -1px 0 #007acc, 1px -1px 0 #007acc, -1px 1px 0 #007acc, 1px 1px 0 #007acc;
    }

    .filtro {
        color: #000;
        text-align: center;
        font-family: 'Times New Roman', Times, serif;
    }
</style>
