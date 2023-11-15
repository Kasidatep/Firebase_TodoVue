<script setup>
import {ref} from 'vue'
import { collection, serverTimestamp, addDoc } from '@firebase/firestore';

import db from '../firebase/init'
import TodoList from './TodoList.vue';
const emit = defineEmits(['update-todos'])
const newTitle = ref('')

const addTodo = async () =>{
    const docRef = await addDoc(collection(db, "todos"),  {
    "createdAt": serverTimestamp(),
    "completed": false,
    "title": newTitle.value,
})
 emit('update-todos')
}

</script>
<template>
    <div class="w-full ">
        <div class="mb-6 flex">
            <input type="text" v-model="newTitle" placeholder="Enter a new task" class="w-96 bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
            <button type="button" @click="addTodo" class="ml-5 text-white bg-gradient-to-r from-teal-400 via-teal-500 to-teal-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-teal-300 dark:focus:ring-teal-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center">Add</button>
        </div>
    </div>
</template>