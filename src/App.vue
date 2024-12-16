<script>
import { ref } from 'vue';
import { onMounted } from "vue";
import PokemonList from './components/PokemonList.vue';

export default {
  components: {
    PokemonList,
  },
  setup() {
    const pokedex = ref([]);
    const pokemonList = ref([]);

    const addPokemon = (pokemon) => {
      if (!pokedex.value.find((p) => p.id === pokemon.id)) {
        pokedex.value.push(pokemon);
      }
    };

    const addRandomPokemon = () => {
      const randomIndex = Math.floor(Math.random() * pokemonList.value.length);
      const randomPokemon = pokemonList.value[randomIndex];
      addPokemon(randomPokemon);
    };

    const removePokemon = (pokemonId) => {
      pokedex.value = pokedex.value.filter((p) => p.id !== pokemonId);
    };

    onMounted(async () => {
      const response = await fetch('https://pokebuildapi.fr/api/v1/pokemon/limit/100');
      pokemonList.value = await response.json();
    });

    return {
      pokedex,
      pokemonList,
      addPokemon,
      addRandomPokemon,
      removePokemon,
    };
  },
};
</script>

<template>
   <div>
    <h1>Mon Pokédex</h1>
    <p>Total capturé : {{ pokedex.length }}</p>

    <div class="main-content">
      <pokemon-list
        :pokemons="pokedex"
        @remove:pokemon="removePokemon"
      />
      <div class="add-button-container">
        <button @click="addRandomPokemon">
          Ajouter des Pokémon à mon Pokédex
        </button>
      </div>
    </div>

    <p v-if="pokedex.length === 0">Votre Pokédex est vide.</p>
  </div>
</template>

<style>
.main-content {
  display: flex;
  gap: 20px;
  align-items: flex-start;
}

.add-button-container button {
  margin-top: 10px;
  padding: 10px;
  font-size: 14px;
  cursor: pointer;
}
</style>