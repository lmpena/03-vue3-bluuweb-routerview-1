<script setup>
    //import { ref } from 'vue';
    import { RouterLink } from  'vue-router'
    //import axios from 'axios';

    import { useGetData } from '@/composables/getData';

    const { getData, data, loading, error } = useGetData();

//    const pokemons = ref ( [] );
//    const getData = async() => {
//        try {
//            const { data } = await axios.get('https://pokeapi.co/api/v2/pokemon');
//            pokemons.value = data.results;
//        } catch (error) {
//            console.log(error);
//        }
//    }
//
//    getData();

    getData('https://pokeapi.co/api/v2/pokemon');

</script>

<template>
    <h1>Pokemons: </h1>
    <p v-if="loading">Cargando información... </p>
    <div class="alert alert-danger mt-2" v-if="error"> {{ error }} </div>
    <div v-if="data">
        <ul class="list-group">
            <li class="list-group-item" v-for="poke in data.results" :key="poke.name">
                <router-link :to="`/pokemons/${poke.name}`"
                > {{ poke.name }} 
                </router-link>
            </li>
        </ul>
        <div class="mt-2">
            <button :disabled="!data.previous" class="btn btn-success me-1" @click="getData(data.previous)">Previous</button>
            <button :disabled="!data.next" class="btn btn-primary" @click="getData(data.next)">Next</button>
        </div>
    </div>
</template>