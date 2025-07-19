<script setup lang="ts">
import TodoItem from './todo-item.vue'

import { ref } from 'vue'

interface TTodo {
  title: string
  isCompleted: boolean
}

const saveTodos = () => {
  localStorage.setItem('todos', JSON.stringify(todos.value))
}

const getTodoList = () => {
  const todosRaw = localStorage.getItem('todos')
  if (!todosRaw) return []
  const todos: TTodo[] = JSON.parse(todosRaw)
  return todos
}

const todos = ref<TTodo[]>(getTodoList())

const toggleTodo = (index: number) => {
  todos.value[index].isCompleted = !todos.value[index].isCompleted
  saveTodos()
}

const deleteTodo = (index: number) => {
  todos.value = todos.value.filter((__, todoIndex) => todoIndex !== index)
  saveTodos()
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
  saveTodos()
}
</script>

<template>
  <div class="todo-container">
    <h1 class="title">This is a ToDo</h1>
    <ul :class="['todo-list', { invisible: todos.length === 0 }]">
      <li v-for="(todo, index) in todos" v-bind:key="index" class="todo-item">
        <TodoItem
          @toggle="toggleTodo(index)"
          @delete="deleteTodo(index)"
          :todo="todo"
        />
      </li>
    </ul>
    <button class="button" v-if="!isInputOpen" type="button" @click="openInput">
      Add Todo
    </button>
    <form class="form" v-else @submit="addTodo">
      <input
        class="form-input"
        v-model="inputValue"
        type="text"
        name="todo"
        id="todo"
        placeholder="What todo?"
      />
      <button class="button" type="submit">Add</button>
    </form>
  </div>
</template>

<style scoped>
.todo-container {
  min-width: 250px;
  padding: 30px;
  border: 2px solid var(--color-border);
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  gap: 40px;
}

.title {
  font-family: sans-serif;
}

.todo-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
  border: 2px solid var(--color-border);
  border-radius: 15px;
  padding: 20px;
}

.invisible {
  display: none;
}

.form {
  display: flex;
  flex-direction: row;
  gap: 20px;
}

.form-input {
  background-color: var(--color-background);
  outline: none;
  border: none;
}

.button {
  background-color: transparent;
  border: 2px solid var(--color-border);
  border-radius: 15px;
  padding: 12px;
  cursor: pointer;
  transition:
    background-color 0.3s ease,
    color 0.3s ease;
}

.button:hover {
  background-color: var(--color-border);
  color: var(--color-background);
}
</style>
