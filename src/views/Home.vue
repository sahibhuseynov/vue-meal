<template>
    <div class="flex flex-col p-8 ">
        <div>
            <input type="text" class="rounded border border-gray-200 w-full" 
        placeholder="Search for Meals">
        </div>
       
        <div class="flex gap-3 mt-2 justify-center">
            <RouterLink :to="{name: 'byLetter', params: {letter}}" v-for="letter in letters" :key="letter">
                {{ letter }}
            </RouterLink>
        </div>

        
    </div>
</template>

<script setup>
import { computed , onMounted,ref} from 'vue';
import store from '../store';
import axiosClient from '../axiosClient.js'


const meals = computed(() => store.state.meals)
const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split('')
const ingredients = ref([])
onMounted(async () => {
   const res = await  axiosClient.get("list.php?i=list")
   ingredients.value = res.data
})
</script>

