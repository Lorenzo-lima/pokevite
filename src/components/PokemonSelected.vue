<script setup>
import { computed } from 'vue';
const pokemon = defineProps(["name", "xp", "height", "img", "loading"])
const capitalizedPokemonName = computed(() => {
  return pokemon.name ? pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1) : null;
});
</script>

<template>
  <div 
  class="card pokemonSelected"
  :class="loading ? '' : 'animate__animated animate__zoomIn'"
  >
    <h3 class="card-title text-center mt-5">{{ capitalizedPokemonName || '???'}}</h3>
    <img
    v-if="pokemon.name"
      height="250"
      :src="pokemon.img"
      class="card-img-top mt-5 pt-2"
      alt="Pokemon Name"
    />
    <img
    v-else
      height="250"
      src="../assets/egg_pokemon.svg"
      class="card-img-top mt-5 pt-2"
      :alt="pokemon.name"
    />
    <div class="card-body">
      <hr />
      <div class="row">
        <section class="col">
          <strong>XP: </strong>
          <span>{{ pokemon.xp }}</span>
        </section>
        <section class="col">
          <strong>Altura: </strong>
          <span> {{ pokemon.height }}</span>
        </section>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .pokemonSelected {
    height: 75vh;
    background: radial-gradient(circle, rgba(50, 43, 185, 0.664) 0%, rgba(72, 90, 255, 0.781) 50%, rgba(68, 27, 143, 0.918) 100%);
  }
</style>
