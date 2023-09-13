<script setup>
import { onMounted, reactive, ref, computed } from "vue"
import ListPokemons from "../components/ListPokemons.vue"
import PokemonSelected from "../components/PokemonSelected.vue"

let urlBaseSvg = ref(
  "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/"
)
let pokemons = reactive(ref())
let searchPokemon = ref("")
let pokemonSelected = reactive(ref())
let loading = ref(false)

onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
    .then((response) => response.json())
    .then((response) => (pokemons.value = response.results))
})

const pokemonsFiltered = computed(() => {
  if (pokemons.value && searchPokemon.value) {
    return pokemons.value.filter((pokemon) =>
      pokemon.name.toLowerCase().includes(searchPokemon.value.toLowerCase())
    )
  }
  return pokemons.value
})

const selectPokemon = async (pokemon) => {
  loading.value = true
  await fetch(pokemon.url)
    .then((response) => response.json())
    .then((response) => (pokemonSelected.value = response))
    .catch(error => alert(error))
    .finally(() => loading.value = false)
}
</script>

<template>
  <main>
    <div class="container">
      <div class="row mt-4">
        <div class="col-sm-12 col-md-6">
          <PokemonSelected
            :name="pokemonSelected?.name"
            :xp="pokemonSelected?.base_experience"
            :height="pokemonSelected?.height"
            :img="pokemonSelected?.sprites.other.dream_world.front_default"
            :loading="loading"
            class="text-light"
          />
        </div>
        <div class="col-sm-12 col-md-6">
          <div class="card cardlist">
            <div class="card-body row">
              <div class="mb-2">
                <label hidden for="searchPokemon" class="form-label"> </label>
                <input
                  v-model="searchPokemon"
                  type="text"
                  class="form-control"
                  id="searchPokemon"
                  placeholder="Pesquisar"
                />
              </div>
              <ListPokemons
                v-for="pokemon in pokemonsFiltered"
                :key="pokemon.name"
                :name="pokemon.name"
                :urlBaseSvg="urlBaseSvg + pokemon.url.split('/')[6] + '.svg'"
                @click="selectPokemon(pokemon)"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.cardlist {
  max-height: 75vh;
  overflow-y: scroll;
  overflow-x: hidden;
}

.cardlist::-webkit-scrollbar {
  width: 5px;
}

.cardlist::-webkit-scrollbar-thumb {
    background-color: rgb(192, 192, 192);
    border-radius: 2px;
}

@media (max-width: 767px) {
  .cardlist {
    margin-top: 20px;
  }
}
</style>
