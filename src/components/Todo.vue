<script setup>
import {query, collection, getDocs} from 'firebase/firestore'
import {ref, onMounted} from 'vue'
import db from '../firebase/init'

const todos = ref([])

const getTodos = async () => {
    const coll = collection(db, 'todos')
    const querySnap = await getDocs(query(coll))
    todos.value = []
    querySnap.forEach((doc) => {
        let data = doc.data()
        data.id = doc.id
        todos.value.push(data)
    })
}

onMounted(()=>{
getTodos()
})
</script>
<template>
<h2 class="mb-2 text-lg font-semibold text-gray-900 dark:text-white">Todo List:</h2>
    <ol class=" space-y-1 text-gray-500 list-decimal list-inside dark:text-gray-400">
       
    <li v-for="todo in todos" :key="todo.title">
        {{todo.title}}
        <button type="button" class="text-gray-900 bg-white border border-gray-300 focus:outline-none hover:bg-gray-100 focus:ring-4 focus:ring-gray-200 font-medium rounded-lg text-sm px-5 py-1 me-2 mb-2">Complete</button>
        <button type="button" class="text-gray-100 bg-red-600 border border-gray-300 focus:outline-none hover:bg-red-700 focus:ring-4 focus:ring-gray-200 font-medium rounded-lg text-sm px-5 py-1 me-2 mb-2">Delete</button>
    </li>
</ol>
</template>
<style>

</style>