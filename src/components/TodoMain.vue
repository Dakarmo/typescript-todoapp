<template>
  <main class="main">
    <!-- <ul class="todo-list">
            <li :class="{competed: todo.complete}" v-for="todo in taches" :key="todo.id">
                <div class="view">
                    <input type="checkbox" class="toggle ">
                    <label for="">{{ todo.title }}</label>
                    <button class="destroy"></button>
                </div>
            </li>
        </ul> -->
    <ul class="todo-list">
      <TodoItem
        v-for="todo in taches"
        :key="todo.id"
        :todo="todo"
        @update-todo="updateTodo"
        @delete-todo="emit('delete-todo', todo)"
        @edit-todo="editTodo"
      />
    </ul>
  </main>
</template>

<script setup lang="ts">
import type { Todo } from '@/@types'
import TodoItem from '@/components/TodoItem.vue'

// const props = defineProps(['taches']);

const props = defineProps<{
  taches: Todo[]
}>()

const emit = defineEmits<{
  (e: 'delete-todo', todo: Todo): void
  (e: 'update-todo', todo: Todo, completeVal: boolean): void
  (e: 'edit-todo', todo: Todo, value: string): void
}>()

function updateTodo(todo: Todo, completedValue: boolean) {
  emit('update-todo', todo, completedValue)
}
function editTodo(todo: Todo, value: string) {
  emit('edit-todo', todo, value)
}
</script>

<style scoped></style>
