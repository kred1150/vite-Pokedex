<script setup>
import { reactive, ref, computed, onMounted } from "vue";
import PokedexCard from "./components/PokedexCard.vue";

const pokemonList = ref([]);
const searchPokemon = ref("");

const pokemonStore = reactive({
  list: [],
  filteredList: computed(() =>
    pokemonStore.list.filter((pokemon) => pokemon.pokemon_species.name.includes(searchPokemon.value))
  ),
});

onMounted(async () => {
  const pokeData = await fetch("https://pokeapi.co/api/v2/pokedex/2/").then((response) => response.json());
  pokemonStore.list = pokeData.pokemon_entries;
});
</script>

<template>
  <h1>Pokedex</h1>

  <p>{{ searchPokemon }}</p>
  <input type="text" v-model="searchPokemon" />

  <PokedexCard
    v-for="pokemon in pokemonStore.filteredList"
    key:pokemon
    :number="pokemon.entry_number"
    :name="pokemon.pokemon_species.name"
  />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
