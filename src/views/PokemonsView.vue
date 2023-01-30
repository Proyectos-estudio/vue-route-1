<script setup>
import { ref } from "@vue/reactivity";
// import axios from "axios";
import { RouterLink } from "vue-router";
import { useGetData } from "@/composables/getData";

const pokemons = ref([]);

const { data, getData, loading, error } = useGetData();

// const getData = async () => {
//   try {
//     const { data } = await axios.get("https://pokeapi.co/api/v2/pokemon");
//     pokemons.value = data.results;
//   } catch (error) {
//     console.log(error);
//   }
// };

getData("https://pokeapi.co/api/v2/pokemon");
</script>

<template>
  <h1>Pokemones</h1>
  <p v-if="loading">Cargando pokemones...</p>
  <div class="alert alert-danger" v-if="error">{{ error }}</div>
  <div v-if="data">
    <ul class="list-group">
      <li v-for="(pokemon, index) in data.results" :key="index" class="list-group-item">
        <router-link :to="`/pokemons/${pokemon.name}`">{{
          pokemon.name
        }}</router-link>
      </li>
    </ul>

    <div class="my-2">
      <button :disabled="!data.previous" class="btn btn-warning me-2" @click="getData(data.previous)">
        Previuos
      </button>
      <button :disabled="!data.next" class="btn btn-primary" @click="getData(data.next)">Next</button>
    </div>
  </div>
</template>
