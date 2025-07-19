<script setup lang="ts">
import TodoItem from './todo-item.vue'

import { ref } from 'vue'

interface TList {
  title: string
  isCompleted: boolean
}

const todos = ref<TList[]>([])

const toggleTodo = (index: number) => {
  todos.value[index].isCompleted = !todos.value[index].isCompleted
}

const deleteTodo = (index: number) => {
  todos.value = todos.value.filter((__, todoIndex) => todoIndex !== index )
}

const isInputOpen = ref<boolean>(false)
const openInput = () => {
  isInputOpen.value = !isInputOpen.value
}
const inputValue = ref<string>('')
const addTodo = (e: Event) => {
  e.preventDefault()
  if (inputValue.value.trim()) {
    todos.value.push({
      title: inputValue.value,
      isCompleted: false,
    })
  }
  inputValue.value = ''
  isInputOpen.value = false
}
</script>

<template>
  <div class="todo-container">
    <h1 class="title">This is a ToDo</h1>
    <ul class="todo-list">
      <li v-for="(todo, index) in todos" v-bind:key="index" class="todo-item">
        <TodoItem @toggle="toggleTodo(index)" @delete="deleteTodo(index)" :todo="todo" />
      </li>
    </ul>
    <button v-if="!isInputOpen" type="button" @click="openInput">Add Todo</button>
    <form v-else @submit="addTodo">
      <input v-model="inputValue" type="text" name="todo" id="todo" placeholder="What todo?" />
      <button type="submit">Add</button>
    </form>
  </div>
</template>

<style scoped></style>