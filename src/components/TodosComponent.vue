<template>
  <div>
    <TodoHeader @add-todo="addTodo" />

    <TodoMain
      :taches="todos"
      @delete-todo="deleteTodo"
      @update-todo="updateTodo"
      @edit-todo="editTodo"
    />

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
import { useStorage } from '@vueuse/core'

// interface Todo {
//     id: number,
//     title: string,
//     complete: boolean,
// }

// const todos = ref<Todo[]>([]);

const todos = useStorage<Todo[]>('todoapp-todos', [])

function addTodo(value: string) {
  //   alert('Youpi !')
  if (value.trim().length === 0) return

  todos.value.push({
    id: nanoid(),
    title: value,
    complete: false
  })
}

function deleteTodo(todo: Todo): void {
  todos.value = todos.value.filter((el) => el !== todo)
}

function updateTodo(todo: Todo, completedValue: boolean) {
  todo.complete = completedValue
}
function editTodo(todo: Todo, value: string) {
  todo.title = value
}
</script>

<style scoped></style>
