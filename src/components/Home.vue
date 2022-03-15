<script setup lang="ts">
import { ref } from "vue";
import { TodoItem } from "../interfaces";
import Maker from "./Maker.vue";
import Todo from "./Todo.vue";

defineProps<{ msg: string }>();

const todosList = ref<TodoItem[]>([]);

const lightMode = ref<boolean>(true);

function handleAdd(todo: TodoItem) {
  todosList.value.push(todo);
}
function handleDelete(index: number) {
  todosList.value.splice(index, 1);
}
function handleDone(index: number) {
  todosList.value[index].done = !todosList.value[index].done;
}
function handleModeSwitch() {
  lightMode.value = !lightMode.value;
  const page = document.querySelector<HTMLElement>("body")!;
  page.style.backgroundColor = lightMode.value ? "#fff" : "#000";
  page.style.color = lightMode.value ? "#fff !important" : "#000";
}
</script>

<template>
  <div id="wrapper">
    <h1>{{ msg }}</h1>
    <h3>
      <button @click="handleModeSwitch">
        {{ lightMode ? "dark mode?" : "light mode?" }}
      </button>
    </h3>
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
  </div>
</template>

<style scoped>
a {
  color: #42b983;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
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
