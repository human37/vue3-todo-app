<script setup lang="ts">
import Maker from "./Maker.vue";
import Todo from "./Todo.vue";
import { ref } from "vue";

defineProps<{ msg: string }>();

interface TodoItem {
  title: string;
  details: string;
  done: boolean;
}

const todosList = ref<TodoItem[]>([]);

function handleAdd(todo: { title: string; details: string }) {
  todosList.value.push({
    title: todo.title,
    details: todo.details,
    done: false,
  });
}
function handleDelete(index: number) {
  todosList.value.splice(index, 1);
}
function handleDone(index: number) {
  todosList.value[index].done = !todosList.value[index].done;
}
</script>

<template>
  <h1>{{ msg }}</h1>
  <section>
    <Maker id="maker" @add="handleAdd" />
  </section>
  <p v-for="todo in todosList">
    <Todo
      id="todo"
      :title="todo.title"
      :details="todo.details"
      :done="todo.done"
      @delete="handleDelete"
      @done="handleDone"
    />
  </p>
</template>

<style scoped>
a {
  color: #42b983;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}
#maker {
  margin-left: auto;
  margin-right: auto;
  border: 1px solid #ccc;
  border-radius: 18px;
  margin-top: 40px;
  width: 400px;
}
#todo {
  margin-left: auto;
  margin-right: auto;
  border: 1px solid #ccc;
  border-radius: 18px;
  max-width: 300px;
  padding: 10px;
}
</style>
