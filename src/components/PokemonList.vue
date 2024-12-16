<script>
  import PokemonCard from './PokemonCard.vue';
  export default {
    components: {
      PokemonCard, },
    props: {
      pokemons: {
        type: Array,
        required: true,
      },
    },
  };
</script>


<template>
    <div>
      <pokemon-card
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        :pokemon="pokemon"
        @remove:pokemon="$emit('remove:pokemon', pokemon.id)"
      />
    </div>
</template> 


<style>
div {
    display: flex;
    flex-wrap: wrap;
    gap: 5px;
    }
</style>