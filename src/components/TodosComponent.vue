<template>
  <div>
    <TodoHeader @add-todo="addTodo" />
    <!-- 
    <TodoMain
      :taches="todos"
      @delete-todo="deleteTodo"
      @update-todo="updateTodo"
      @edit-todo="editTodo"
    /> -->

    <TodoMain
      :taches="filteredTodos"
      @delete-todo="deleteTodo"
      @update-todo="updateTodo"
      @edit-todo="editTodo"
      @toggle-all-input = "toggleAllInput"
    />

    <TodoFooter :todos="todos" @delete-completed="deleteCompleted" />

    <!-- <pre>waiting {{ waitingTodos }}</pre>
    <pre>completed {{ completedTodos }}</pre> -->
    <!-- <pre>filtered {{ filteredTodos }}</pre> -->
  </div>
  <!-- <pre>{{ todos }}</pre> -->
</template>

<script setup lang="ts">
import TodoHeader from '@/components/TodoHeader.vue'
// import TodoHeader from './TodoHeader.vue';
import TodoMain from '@/components/TodoMain.vue'
import TodoFooter from '@/components/TodoFooter.vue'
import type { Todo } from '@/@types'
import { computed, ref } from 'vue'
import { nanoid } from 'nanoid'
import { useStorage } from '@vueuse/core'
import { useRoute } from 'vue-router'

// interface Todo {
//     id: number,
//     title: string,
//     complete: boolean,
// }

// const todos = ref<Todo[]>([]);
const todos = useStorage<Todo[]>('todoapp-todos', [])

const route = useRoute()

const filters = computed(() => {
  return {
    all: todos,
    waiting: todos.value.filter((el) => !el.complete),
    completed: todos.value.filter((el) => el.complete)
  }
})

const waitingTodos = computed<Todo[]>(() => filters.value.waiting)
const completedTodos = computed<Todo[]>(() => filters.value.completed)

const filteredTodos = computed(() => {
  switch (route.name) {
    case 'waiting':
      return waitingTodos.value
    case 'completed':
      return completedTodos.value
    default:
      return todos.value
  }
})

function addTodo(value: string) {
  //   alert('Youpi !')
  if (value.trim().length === 0) return

  todos.value.push({
    id: nanoid(),
    title: value,
    complete: false
  })
}
function toggleAllInput(value: boolean){
  // alert("toggleAllInput: value = " + value);
  todos.value.forEach((todo) => {
    todo.complete = value;
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

function deleteCompleted(): void {
  todos.value = todos.value.filter((el) => !el.complete)
}
</script>

<style scoped></style>
