<script setup>
  const pokemon = defineProps(['name', 'id', 'types']);
</script>


<template>
  <div class="col-4">
    <div class="card mb-3">
      <img class="card-img-top" :src="'https://assets.pokemon.com/assets/cms2/img/pokedex/detail/' + pokemon.id.toString().padStart(3, '0') + '.png'" alt="Card image">
      <div class="card-body d-flex flex-column justify-content-center align-items-center">
        <h5 class="card-title text-center text-capitalize">{{ pokemon.name }}</h5>
        <p class="card-text text-center">Descubra mais sobre o Pokémon {{ pokemon.name }} em nossa pokédex</p>
        </div>
      </div>
    </div>
</template>


<style></style>
