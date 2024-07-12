<template>
  <footer class="footer">
    <span class="todo-count">
      <strong>{{ remaining }}</strong> tâche{{ remaining > 1 ? 's' : '' }} restante{{
        remaining > 1 ? 's' : ''
      }}
    </span>
    <ul class="filters">
      <li>
        <routerLink to="#">Tous</routerLink>
      </li>
      <li>
        <routerLink to="#">En cours</routerLink>
      </li>
      <li>
        <routerLink to="#">Terminés</routerLink>
      </li>
    </ul>
    <button class="clear-completed">Eff. tâche terminées</button>
  </footer>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const remaining = ref<number>(3)
</script>

<style scoped></style>
