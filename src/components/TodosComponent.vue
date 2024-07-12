<template>
  <div>
    <TodoHeader @add-todo="addTodo" />

    <TodoMain :taches="todos" />

    <TodoFooter :todos="todos" />
  </div>
</template>

<script setup lang="ts">
import TodoHeader from '@/components/TodoHeader.vue'
// import TodoHeader from './TodoHeader.vue';
import TodoMain from '@/components/TodoMain.vue'
import TodoFooter from '@/components/TodoFooter.vue'
import type { Todo } from '@/@types'
import { ref } from 'vue';

// interface Todo {
//     id: number,
//     title: string,
//     complete: boolean,
// }

const todos = ref<Todo[]>([
 
])

function addTodo(value: string) {
//   alert('Youpi !')
todos.value.push({
    id: 0,
    title: value,
    complete: false
})
}
</script>

<style scoped></style>
