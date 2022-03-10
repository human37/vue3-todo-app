<script setup lang="ts">
defineProps<{ title: string; details: string; done: boolean }>();
</script>

<template>
  <div>
    <header>
      <button @click="$emit('delete')">X</button>
      <label for="checkbox">done?</label>
      <input
        v-model="done"
        type="checkbox"
        name="checkbox"
        @click="$emit('done')"
      />
    </header>
    <h1>{{ title }}</h1>
    <body>
      {{ details }}
    </body>
  </div>
</template>

<style scoped>
button {
  margin-right: 10px;
  height: 30px;
  width: 30px;
  border: none;
  border-radius: 18px;
  cursor: pointer;
  float: left;
}
input,
label {
  float: right;
}
h1 {
  border-bottom: 1px solid #ccc;
}
</style>
