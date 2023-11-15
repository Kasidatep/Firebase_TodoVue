<script setup>
import {query, collection, getDocs, getDoc, doc, deleteDoc, updateDoc} from 'firebase/firestore'
import {ref, onMounted} from 'vue'
import db from './firebase/init'

import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
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

const toggleCompleted = async (id) => {
  const docRef = doc(db,'todos',id)
  const item = await getDoc(docRef)
  const data = item.data()
  await updateDoc(docRef, {'completed':!data.completed})
  await getTodos()
}

const deleteTodo = async (id) => {
  await deleteDoc(doc(db,'todos',id))
  await getTodos()
}

onMounted(()=>{
getTodos()
})

const updateTodo = () => {
  getTodos()
}
</script>

<template>
  <main class="m-5">
    <h1 class="mb-2 text-2xl font-extrabold text-gray-900 dark:text-white">Todo List:</h1>
    <TodoInput @update-todos="updateTodo"/>
    <TodoList :todos="todos" @delete-todo="deleteTodo" @togle-completed="toggleCompleted"/>
  </main>
</template>

<style scoped>

</style>
