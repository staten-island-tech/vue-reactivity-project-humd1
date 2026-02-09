<script setup>
import {ref} from 'vue'
import ListCard from '@/components/ListCard.vue';
const lists = ref([
  { name: "Placeholder", tasks: ["Placeholder Task 1", "Placeholder Task 2"] },
])
</script>


<template>
  <div class = "headings flex flex-col gap-2 mt-8 text-center items-center">
  <h1 class = "text-6xl font-gummy text-black text-shadow-md tracking-widest">To Do!</h1>
  <h2 class = "text-4xl font-fancy text-sky-200 tracking-wide">do yo work</h2>
  <hr class="border-gray-400 border-1 border-dotted w-300 my-4">
  </div>

  
  <h2 class = "your lists text-5xl font-gummy text-sky-200 tracking-wide text-center">Your Lists:</h2>
  <div class = "listcontainer flex justify-center mt-10">
  <ListCard v-for= "list in lists" :key="list.name" :list="list">{{list.name}}</ListCard> 
  </div>
</template>

<style scoped></style>
