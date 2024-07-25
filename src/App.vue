<script setup>
import { ref, onMounted, computed, reactive } from "vue";
import PokeCard from './components/PokeCard.vue'
const pokemonList = ref([])
const filterText = ref('')

const pokemonStore = reactive({
  list: [],
  filteredList: computed (() => { 
    return pokemonStore.list.filter( pokemon => {
      return pokemon.pokemon_species.name.includes(filterText.value)
    })
  })
})

onMounted(async () => {
  const pokeData = await fetch(
    'https://pokeapi.co/api/v2/pokedex/2/'
  ).then(
    response => response.json()
  )

  //pokemonList.value = pokeData.pokemon_entries
  pokemonStore.list = pokeData.pokemon_entries

})
</script>

<template>
  <h1>PokeApp</h1>
  <span>Search </span> 
  <input type="text" v-model="filterText" />
  <ul>
    <PokeCard 
      v-for="( pokemon, index ) in pokemonStore.filteredList" 
      :key="`poke-${{ index }}`"
      :number="pokemon.entry_number"
      :name="pokemon.pokemon_species.name"
    />
  </ul>
</template>

<style scoped>
body{
  margin: 0;
}

ul {
  list-style-type: none;
  margin: 0;
  padding: 20px 0;
}

</style>
