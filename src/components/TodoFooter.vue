<template>
  <footer v-if="todos.length > 0" class="footer">
    <span class="todo-count">
      <strong>{{ remaining }}</strong> tâche{{ remaining > 1 ? 's' : '' }} restante{{
        remaining > 1 ? 's' : ''
      }}
    </span>
    <ul class="filters">
      <li>
        <routerLink :class="{ selected: route.path === '/' }" to="/">Tous</routerLink>
      </li>
      <li>
        <routerLink :class="{ selected: route.path === '/waiting' }" to="/waiting"
          >En cours</routerLink
        >
      </li>
      <li>
        <routerLink :class="{ selected: route.path === '/completed' }" to="/completed"
          >Terminés</routerLink
        >
      </li>
    </ul>
    <button
      class="clear-completed"
      @click="emit('delete-completed')"
      v-show="todos.some((todo) => todo.complete)"
    >
      Eff. tâche terminées
    </button>
  </footer>
</template>

<script setup lang="ts">
import type { Todo } from '@/@types'
import { computed } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()

const props = defineProps<{
  todos: Todo[]
}>()
const remaining = computed(() => props.todos.filter((el) => !el.complete).length)

const emit = defineEmits<{
  (e: 'delete-completed'): void
}>()
</script>

<style scoped></style>
