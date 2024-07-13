<template>
  <div>
    <TodoHeader @add-todo="addTodo" />

    <TodoMain :taches="todos" @delete-todo="deleteTodo" />

    <TodoFooter :todos="todos" />
  </div>
  <!-- <pre>{{ todos }}</pre> -->
</template>

<script setup lang="ts">
import TodoHeader from '@/components/TodoHeader.vue'
// import TodoHeader from './TodoHeader.vue';
import TodoMain from '@/components/TodoMain.vue'
import TodoFooter from '@/components/TodoFooter.vue'
import type { Todo } from '@/@types'
import { ref } from 'vue'
import { nanoid } from 'nanoid'

// interface Todo {
//     id: number,
//     title: string,
//     complete: boolean,
// }

const todos = ref<Todo[]>([])

function addTodo(value: string) {
  //   alert('Youpi !')
  todos.value.push({
    id: nanoid(),
    title: value,
    complete: false
  })
}

function deleteTodo (todo: Todo ): void{
  todos.value = todos.value.filter(el => el !== todo);
}
</script>

<style scoped></style>
