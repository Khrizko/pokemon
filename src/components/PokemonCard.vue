<script>
  export default {
    props: {
      pokemon: {
        type: Object,
        required: true,
      },
    },
    methods: {
      showDetails() {
        alert(`Nom: ${this.pokemon.name}\n
        ID: ${this.pokemon.id}\n
        Type: ${this.pokemon.apiTypes.map(t => t.name).join(', ')}`);
      },
    },
  };
</script>
  

<template>
    <div class="pokemon-card">
      <img :src="pokemon.image" :alt="pokemon.name" />
      <h3>{{ pokemon.name }}</h3>
      <button @click="$emit('remove:pokemon', pokemon.id)">Retirer</button>
      <button @click="showDetails">Détails</button>
    </div>
  </template>
   
  
<style>
  .pokemon-card {
    border: 5px solid rgb(19, 0, 128);
    padding: 10px;
    text-align: center;
    width: 100px;
  }
  
  .pokemon-card img {
    max-width: 100%;
    height: auto;
  }
</style>