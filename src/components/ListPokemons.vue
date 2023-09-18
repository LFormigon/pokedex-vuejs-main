<template>
    <div class="col-4">
      <div class="card mb-3">
        <img class="card-img-top" :src="'https://assets.pokemon.com/assets/cms2/img/pokedex/detail/' + pokemonId + '.png'" alt="Card image">
        <div class="card-body d-flex flex-column justify-content-center align-items-center">
          <h5 class="card-title text-center text-capitalize">{{ pokemonData ? pokemonData.name : 'Carregando...' }}</h5>
          <p class="card-text text-center">Descubra mais sobre o Pokémon {{ pokemonData ? pokemonData.name : 'Carregando...' }} em nossa pokédex</p>
          <button class="btn btn-dark" @click="showAbilities = !showAbilities">Detalhes</button>
          <!-- Exibir informações de gênero e habilidades quando showAbilities for verdadeiro -->
          <div v-if="showAbilities">
            <p class="text-center">Gênero: {{ getpokemonGender() }}</p>
            <p class="text-center">Habilidades:</p>
            
  
            <ul class="text-center">
              <li v-for="(ability, index) in abilitiesData" :key="index">{{ ability.name }}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps, ref, onMounted } from 'vue';
  
  const pokemon = defineProps(['name', 'link', 'abilities', 'gender']);
  const pokemonId = pokemon.link.split("/")[6].toString().padStart(3, '0');
  const showAbilities = ref(false);
  
  const pokemonData = ref(null);
  const abilitiesData = ref([]);
  
  const fetchPokemonData = async () => {
    try {
      const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${pokemonId}/`);
      const data = await response.json();
      pokemonData.value = data;
    } catch (error) {
      console.error("Erro ao buscar informações do Pokémon", error);
    }
  };
  
  const fetchAbilitiesData = async () => {
    try {
      const abilities = pokemon.abilities.map((ability) => ability.ability.url);
      const response = await Promise.all(abilities.map((url) => fetch(url)));
      const data = await Promise.all(response.map((res) => res.json()));
      abilitiesData.value = data;
    } catch (error) {
      console.error("Erro ao buscar informações de habilidades do Pokémon", error);
    }
  };
  
  const getpokemonGender = () => {
    return pokemonData ? (pokemonData.gender ? pokemonData.gender.name : 'Desconhecido') : 'Desconhecido';
  };
  
  onMounted(() => {
    fetchPokemonData();
    fetchAbilitiesData();
  });
  </script>
  
  <style></style>