<script>
export default {
  data: () => ({
    pokemonList: [],
  }),
  async mounted() {
    const pokeData = await fetch("https://pokeapi.co/api/v2/pokedex/2/").then((response) => response.json());
    this.pokemonList = pokeData.pokemon_entries;
  },
};
</script>

<template>
  <h1>Pokedex</h1>

  <li v-for="pokemon in pokemonList" key:pokemon>
    ID: {{ pokemon.entry_number }} Name: {{ pokemon.pokemon_species.name }}
  </li>
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
