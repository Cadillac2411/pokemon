
<template>
  <div class="filtro">
    <input class="inputFiltro" v-model="searchTerm" @input="updateSearchTerm" placeholder="Buscar por nombre o ID" />
  </div>
</template>

<script>
  export default {
    data() {
      return {
        searchTerm: '',
      };
    },
    methods: {
      updateSearchTerm() {
        // console.log('updateSearchTerm exec')
        this.$emit('update-search-term', this.searchTerm);
      },
    },
  };
</script>

<style>
  input {
    text-align: center;
    border-color: #000;
    font-size: 16px;
  }

  .inputFiltro{
    border-color: #000;
    font-size: 30px;
  }

  .filtro {
    color: #000;
    text-align: center;
    font-family: 'Times New Roman', Times, serif;
    font-size: 15px;
    margin-top: 0rem;
    margin-bottom: 1rem;
    
  }
</style>
