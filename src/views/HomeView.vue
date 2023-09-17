<script setup>
import { onMounted, reactive, ref } from 'vue';
import ListPokemons from '../components/ListPokemons.vue'


let pokemons = reactive(ref());

onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon/?limit=30&offset=0")
  .then(res => res.json())
  .then(res => {
    pokemons.value = res.results;
    console.log(res)
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
              <ListPokemons 
                v-for="pokemon in pokemons"
                :key="pokemon.name"
                :name="pokemon.name"
                :link="pokemon.url"
                :showDetails="pokemon.showDetails"
              />
            </div>
          </div>
        </div>
      </div>
  </main>
</template>
