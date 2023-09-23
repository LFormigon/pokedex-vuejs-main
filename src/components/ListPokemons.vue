<script setup>
  import { ref } from 'vue';
  const pokemon = defineProps({
    value: Object
  });
  const showDetails = ref(false);

</script>


<template>
  <div class="col-4">
    <div class="card mb-3">
      <img class="card-img-top" :src="'https://assets.pokemon.com/assets/cms2/img/pokedex/detail/' + pokemon.value.id.toString().padStart(3, '0') + '.png'" alt="Card image">
      <div class="card-body d-flex flex-column justify-content-center align-items-center">
        <h5 class="card-title text-center text-capitalize">{{ pokemon.value.name }}</h5>
        <p class="card-text text-center">Descubra mais sobre o Pokémon {{ pokemon.value.name }} em nossa pokédex</p>
        <button class="btn btn-dark" @click="showDetails = !showDetails">Detalhes</button>
        <div v-if="showDetails">
          <div class="card text-white bg-danger mb-3" style="max-width: 18rem;">
            <div class="card-header d-flex"></div>
            <div class="card-body dark">
              <h5 class="card-title text-center text-capitalize">{{ pokemon.value.name }} Possui o Elemento:</h5>
              <h5 class="card-header text-center text-capitalize">{{ pokemon.value.types[0].name }}</h5>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>



<style></style>
