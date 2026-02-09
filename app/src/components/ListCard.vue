<template>
    <div class="listcard flex flex-col bg-white p-4 gap-4 rounded shadow border-2 border-slate-300 justify-between text-center l-50 w-50">
        <h2 class="text-2xl font-gummy text-black-200 tracking-wide">{{ list.name }}</h2>
        <h3 class="text-1xl font-gummy text-sky-200 tracking-wide">{{ list.tasks.length }} tasks</h3>
        <ul class="tasks list-disc list-inside text-center">
            <li v-for="task in list.tasks" :key="task">{{ task }}</li>
        </ul>
        <div class="buttons flex flex-col gap-4">
        <button class="bg-sky-200 hover:bg-sky-300 text-white font-bold py-2 px-4 rounded">View</button>
        <button class="bg-rose-200 hover:bg-rose-300 text-white font-bold py-2 px-4 rounded">Delete</button>
        </div>
    </div>
</template>

<script setup>
defineProps({
    list:{
        type: Object,
        required: true
    }
})
</script>

<style lang="scss" scoped>

</style>