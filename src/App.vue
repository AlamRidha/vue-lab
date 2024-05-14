<template>
  <div class="todo-app">
    <form @submit.prevent="addTodo" class="todo-form">
      <input v-model="newTodo" required placeholder="Masukkan TODO" class="todo-input">
      <button type="submit" class="todo-button">Add Todo</button>
    </form>

    <ul class="todo-list">
      <li v-for="todo in  filteredTodos" :key="todo.id" class="todo-item">
        <input type="checkbox" v-model="todo.done">
        <span :class="{ done: todo.done }">{{ todo.text }}</span>
        <button @click="removeTodo(todo)" class="delete-button">X</button>
      </li>
    </ul>

    <button @click="hideCompleted = !hideCompleted" class="toggle-completed">
      {{ hideCompleted ? 'Show all' : 'Hide completed' }}
    </button>

    <p>{{ pesan }}</p>
  </div>
</template>

<script setup>
import { ref, computed, onUpdated, watch } from 'vue'

const pesan = ref("Inputan kosong")

onUpdated(() => {
  console.log("Ada suatu perubahan terjadi di website")
})

let id = 0
const newTodo = ref('')
const hideCompleted = ref(false)

watch(newTodo, (data) => {
  if (!isNaN(data)) {
    pesan.value = "Inputan gak boleh diisi dengan angka"
  } else {
    pesan.value = "Inputan diterima"
  }
})


const todos = ref([
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn CSS', done: false },
  { id: id++, text: 'Learn JavaScript', done: true },
  { id: id++, text: 'Learn Vue', done: false }
])

// Manipulasi Data/ array, object
const filteredTodos = computed(() => {
  return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value
})

// Biasanya digunakan untuk button
function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}
</script>

<style>
.todo-input {
  margin: 0 20px 5px 1px;
  padding: 5px;
}

.todo-button {
  color: white;
  background-color: green;
  padding: 4px;
  border-radius: 4px;
  cursor: pointer;
}

.delete-button {
  margin-left: 13px;
  color: white;
  background-color: red;
  cursor: pointer;
}

.done {
  text-decoration: line-through;
  color: blue;

}
</style>