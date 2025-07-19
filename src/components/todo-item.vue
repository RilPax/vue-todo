<script setup lang="ts">
defineProps<{
  todo: {
    title: string
    isCompleted: boolean
  }
}>()

const emit = defineEmits<{
    (e: 'toggle'): void,
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
    <span :class="['title', { completed: !todo.isCompleted }]">{{ todo.title }}</span>
    <button type="button" class="button" @click="handleTodo"></button>
    <button type="button" @click="HandleDelete"></button>
  </div>
</template>

<style scoped></style>
