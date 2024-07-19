<template>
  <footer v-if="todos.length > 0" class="footer">
    <span class="todo-count">
      <strong>{{ remaining }}</strong> tâche{{ remaining > 1 ? 's' : '' }} restante{{
        remaining > 1 ? 's' : ''
      }}
    </span>
    <ul class="filters">
      <li>
        <routerLink to="/">Tous</routerLink>
      </li>
      <li>
        <routerLink to="/waiting">En cours</routerLink>
      </li>
      <li>
        <routerLink to="/completed">Terminés</routerLink>
      </li>
    </ul>
    <button class="clear-completed">Eff. tâche terminées</button>
  </footer>
</template>

<script setup lang="ts">
import type { Todo } from '@/@types'
import { computed } from 'vue'
const props = defineProps<{
  todos: Todo[]
}>()
const remaining = computed(() => props.todos.filter((el) => !el.complete).length)
</script>

<style scoped></style>
