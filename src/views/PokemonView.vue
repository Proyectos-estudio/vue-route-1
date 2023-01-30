<script setup>
// import axios from 'axios';
// import { ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import router from '../router';

import { useGetData } from '@/composables/getData';

const {data, getData, loading, error} = useGetData();

//empuja a una ruta en especifico
const back = () =>{
    router.push('/pokemons')
}
//obtiene los parametros
const route = useRoute();

// const poke = ref({});


// const getPoke = async () => {
//     try {
//         const {data} =  await axios.get(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`)
//         poke.value = data;
//     } catch (error) {
//         console.log(error);
//         poke.value = null;
//     }
// }

getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`);

</script>

<template>
    <h1>Pokemon</h1>
    <p v-if="loading">Cargando pokemon...</p>
  <div class="alert alert-danger my-2" v-if="error">{{ error }}</div>
    <div v-if="data" class="container">
        <img :src="data?.sprites?.front_default" alt="">
        <h1>pokemon : {{ $route.params.name }}</h1>
    </div>
    <button @click="back">Volver</button>
</template>