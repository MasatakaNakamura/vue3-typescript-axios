<template>
  <div>
    <input type="number" v-model="todoId" />
    <p v-if="!todoData">Loading...</p>
    <pre v-else>{{ todoData }}</pre>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'
import axios from 'axios'

const todoId = ref(1)
const todoData = ref(null)

function getTodo() {
  const url = 'https://jsonplaceholder.typicode.com/todos/' + todoId.value
  todoData.value = null
  if (todoId.value > 10) {
    todoId.value = 1
  }
  axios
    .get(url)
    .then((response) => (todoData.value = response.data))
    .catch((error) => console.log(error))
}
getTodo()
watch(todoId, getTodo)

setInterval(() => todoId.value++, 1000 * 3)
</script>

<style scoped></style>
