<template>
  <header class="header">
    <RouterLink>
      <h1>Todos</h1>
    </RouterLink>

    <input
      class="new-todo"
      type="text"
      placeholder="Entrer une tâche"
      autofocus
      autocomplete="off"
      @keyup.enter="
        emit('add-todo', ($event.target as HTMLInputElement).value)
        ;($event.target as HTMLInputElement).value = ''
      "
    />
  </header>
</template>

<script setup lang="ts">
const emit = defineEmits<{
  (event: 'add-todo', value: string): void
}>()
</script>

<style scoped></style>
