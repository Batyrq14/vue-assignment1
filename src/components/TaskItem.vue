<template>
  <li :class="{ completed: task.completed }">
    <span>{{ task.text }} ({{ task.priority }}, {{ task.category }})</span>
    <button @click="$emit('toggle-complete')">Mark as {{ task.completed ? 'Incomplete' : 'Completed' }}</button>
    <button @click="$emit('delete-task')">Delete</button>
  </li>
</template>

<script setup>
defineProps({
  task: Object
});

defineEmits(['toggle-complete', 'delete-task']);
</script>

<style scoped>
li { display: flex; justify-content: space-between; align-items: center; padding: 10px; border-bottom: 1px solid #ddd; }
.completed { text-decoration: line-through; color: gray; }
button { margin-left: 10px; padding: 5px 10px; }
</style>
