<script setup>
import { onMounted, reactive, ref } from 'vue';
import ListPokemons from '../components/ListPokemons.vue'




let pokemons = reactive(ref([]));


onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon/?limit=9&offset=0")
    .then(pokemonsList => pokemonsList.json())
    .then(pokemonsList => {
      pokemonsList.results.map((e) => {
        fetch("https://pokeapi.co/api/v2/pokemon/" + e.name)
          .then(pokemonDetails => pokemonDetails.json())
          .then(pokemonDetails => {
            pokemons.value.push({
              name: pokemonDetails.name,
              id: pokemonDetails.id,
              types: pokemonDetails.types.map((e) => e.type),
            })


            console.log(pokemons.value)
          })
      })
    })


});


</script>


<template>
  <v-row>
    <v-container>
      <h1 class="text-center white--text mb-2" style="font-size: 5rem">
        Pokédex
      </h1>
      <h1 class="text-center white--text mb-8">
        Created by
        <a class="red--text" href="https://github.com/LFormigon">Formigon</a>
      </h1>
    </v-container>
  </v-row>


  <main>
    <div class="container">
      <div class="d-flex justify-content-center align-items-center">
        <div class="col-sm-12 col-md-7">
          <div class="card-body row">
            <ListPokemons v-for="pokemon in pokemons" :key="pokemon.name" :name="pokemon.name" :id="pokemon.id" />
          </div>
        </div>
      </div>
    </div>
  </main>
</template>






<style>
.red--text {
  color: red;
}


.white--text {
  color: white;


}
</style>
