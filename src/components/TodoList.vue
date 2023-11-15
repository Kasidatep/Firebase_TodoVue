<script setup>
import {query, collection, getDocs} from 'firebase/firestore'
import {ref, onMounted} from 'vue'
import db from '../firebase/init'

defineProps(['todos'])
defineEmits(['togle-completed', 'delete-todo'])

</script>
<template>
    <ol class="space-y-1 text-gray-500 list-decimal list-inside dark:text-gray-400">
    <li v-for="todo in todos" :key="todo.title" class="flex">
        <div class="mr-5 w-80" :class="todo.completed?'text-gray-400 line-through':'text-gray-800'">{{todo.title}}</div>
        <button type="button" @click="$emit('togle-completed', todo.id)" class="text-gray-900 bg-white border border-gray-300 focus:outline-none hover:bg-gray-100 focus:ring-4 focus:ring-gray-200 font-medium rounded-lg text-sm px-5 py-1 me-2 mb-2">
            {{todo.completed?'Not Complete':'Complete'}}
        </button>
        <button type="button" @click="$emit('delete-todo', todo.id)" class="text-gray-100 bg-red-600 border border-gray-300 focus:outline-none hover:bg-red-700 focus:ring-4 focus:ring-gray-200 font-medium rounded-lg text-sm px-5 py-1 me-2 mb-2">Delete</button>
    </li>
</ol>
</template>
<style>

</style>