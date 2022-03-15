<script setup lang="ts">
import { ref } from "vue";
import { TodoItem } from "../interfaces";
const title = ref("");
const details = ref("");

const emit = defineEmits(["add"]);

function postTodo() {
  const todo: TodoItem = {
    title: title.value,
    details: details.value,
    done: false,
  };
  emit("add", todo);
  title.value = "";
  details.value = "";
}
</script>

<template>
  <div>
    <h2>make a todo here:</h2>
    <p>
      <label for="title">title:</label>
      <input v-model="title" type="text" name="title" id="title" />
    </p>
    <p>
      <label for="details">details:</label>
      <input v-model="details" type="text" name="details" id="details" />
    </p>
    <p>
      <button @click="postTodo">Add</button>
    </p>
  </div>
</template>

<style scoped>
#wrapper {
  margin-top: 40px;
  border: 1px solid #ccc;
  border-radius: 18px;
}
label {
  padding: 10px;
}
input {
  width: 200px;
}
p {
  padding: 10px;
}
button {
  border: none;
  border-radius: 18px;
  cursor: pointer;
  padding: 10px;
}
</style>
