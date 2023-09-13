<script setup>
import { computed } from 'vue';
const pokemon = defineProps(["name", "urlBaseSvg"])
const capitalizedPokemonName = computed(() => {
  return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1);
});
</script>

<template>
  <div class="col-4">
    <div class="card mb-2 cardlist">
      <p class="text-center text-light">{{ capitalizedPokemonName }}</p>
      <img
        :src="urlBaseSvg"
        class="card-img-topw"
        alt="Pokemon Image"
        height="100"
      />
    </div>
  </div>
</template>

<style scoped>
.cardlist {
  background: radial-gradient(circle, rgba(50, 43, 185, 0.664) 0%, rgba(72, 90, 255, 0.781) 50%, rgba(68, 27, 143, 0.918) 100%);
  cursor: pointer;
}

.cardlist:hover {
  background: radial-gradient(circle, rgba(50, 43, 185, 0.664) 0%, rgba(72, 90, 255, 0.781) 50%, rgba(63, 29, 126, 0.952) 100%);
  transition: 1s;
}

.cardlist img:hover {
  padding: .8px;
}

.cardlist img {
  margin-bottom: 30px;
}
</style>
