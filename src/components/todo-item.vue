<script setup lang="ts">
import { X, Check, Trash } from 'lucide-vue-next'

defineProps<{
  todo: {
    title: string
    isCompleted: boolean
  }
}>()

const emit = defineEmits<{
  (e: 'toggle'): void
  (e: 'delete'): void
}>()

const handleTodo = () => {
  emit('toggle')
}
const HandleDelete = () => {
  emit('delete')
}
</script>

<template>
  <div class="todo">
    <span :class="['title', { completed: todo.isCompleted }]">{{
      todo.title
    }}</span>
    <div class="buttons-container">
      <button type="button" class="button" @click="handleTodo">
        <X v-if="todo.isCompleted" :size="24" />
        <Check v-else :size="24" />
      </button>
      <button type="button" class="button" @click="HandleDelete">
        <Trash :size="24" />
      </button>
    </div>
  </div>
</template>

<style scoped>
.todo {
  display: flex;
  justify-content: space-between;
  border: 2px solid var(--color-border);
  border-radius: 15px;
  align-items: center;
  padding: 5px 5px;
}

.buttons-container {
  display: flex;
  gap: 5px;
}

.button {
  background-color: transparent;
  border: none;
}

.completed {
  color: var(--color-border);
}
</style>
