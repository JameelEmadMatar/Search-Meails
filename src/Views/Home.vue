<template>
    <div class="flex flex-col p-8">
        <h1 class="text-4xl font-bold mb-2 ml-8">Random Meals</h1>
        <Meals :meals="meals"/>
    </div>
</template>

<script setup>
import { onMounted , ref} from 'vue';
import axiosClient from '../axiosClient'
import Meals from '../Compontents/Meals.vue'

const meals = ref([]);
onMounted(async () => {
    for(let i=0 ; i < 25 ; i++){
        axiosClient.get('/random.php')
        .then(({data})=>{
            meals.value.push(data.meals[0])
        });
    }
})
/*
        <router-link 
            :to="{
                name: 'byIngredients', 
                params: {ingredients: ingredient.strIngredient},
            }"
            v-for="ingredient of ingredients" 
            :key="ingredient.idIngredient" 
            class="block bg-white rounded p-3 mb-6 shadow "
            >
            <h3 class="text-2xl font-bold mb-2">{{ingredient.strIngredient}}</h3>
            <p>{{ingredient.strDescription}}</p>
        </router-link>
        */
</script>