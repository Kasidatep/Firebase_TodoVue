<script setup>
defineProps(['todos'])
defineEmits(['togle-completed', 'delete-todo'])
</script>
<template>
    <ol class="space-y-1 text-gray-500 list-decimal list-inside dark:text-gray-400">
        <li v-for="todo in todos" :key="todo.title" class="flex justify-between">
            <div class="mr-5 w-80 pl-2" :class="todo.completed ? 'text-gray-400 line-through' : 'text-gray-800'">{{ todo.title }}</div>
            <div class="">
                <button type="button" @click="$emit('togle-completed', todo.id)"
                    class="w-32 text-gray-900 bg-white border border-gray-300 focus:outline-none hover:bg-gray-100 focus:ring-4 focus:ring-gray-200 font-medium rounded-lg text-sm px-5 py-1 me-2 mb-2">
                    {{ todo.completed ? 'Uncomplete' : 'Complete' }}
                </button>
                <button type="button" @click="$emit('delete-todo', todo.id)"
                    class="text-gray-100 bg-red-600 border border-gray-300 focus:outline-none hover:bg-red-700 focus:ring-4 focus:ring-gray-200 font-medium rounded-lg text-sm px-5 py-1 me-2 mb-2">Delete</button>
            </div>

        </li>
    </ol>
</template>
<style></style>