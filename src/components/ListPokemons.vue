<script setup>
import { ref } from 'vue';

const pokemon = defineProps(['name', 'link', 'abilities']);
const pokemonId = pokemon.link.split("/")[6].toString().padStart(3, '0');
const pokemonAbilities = ref([]);
const showAbilities = ref(false);
</script>

<template>
    <div class="col-md-4">
      <div class="card mb-3">
        <img :src="'https://assets.pokemon.com/assets/cms2/img/pokedex/detail/' + pokemonId + '.png'" class="card-img-top" alt="Imagem do Pokémon">
        <div class="card-body">
          <h5 class="card-title text-center text-capitalize">{{ pokemon.name }}</h5>
          <p class="card-text text-center">Descubra mais sobre o Pokémon {{ pokemon.name }} em nossa Pokédex.</p>
          <a :href="pokemon.link" class="btn btn-dark d-block mx-auto">Detalhes</a>
        </div>
      </div>
    </div>
  </template>
  

<style></style>