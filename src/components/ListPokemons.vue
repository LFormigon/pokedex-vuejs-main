<script setup>
import { ref } from 'vue';

const pokemon = defineProps(['name', 'link', 'abilities']);
const pokemonId = pokemon.link.split("/")[6].toString().padStart(3, '0');
const pokemonAbilities = ref([]);
const showAbilities = ref(false);
</script>

<template>
    <div class="col-4">
        <div class="card mb-3">
            <img class="card-img-top" :src="'https://assets.pokemon.com/assets/cms2/img/pokedex/detail/' + pokemonId + '.png'" alt="Card image">
            <div class="card-body d-flex flex-column  justify-content-center align-items-center">
                <h5 class="card-title text-center text-capitalize">{{ pokemon.name }}</h5>
                <p class="card-text text-center">Descubra mais sobre o pokemon {{ pokemon.name }} em nossa pokédex</p>
                <a :href="pokemon.link" class="btn btn-dark">Detalhes</a>
            </div>
        </div>
    </div>
</template>

<style></style>