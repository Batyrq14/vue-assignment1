<template>
  <li :class="{ completed: task.completed }" class="task-item">
    <span>{{ task.text }} ({{ task.priority }}, {{ task.category }})</span>
    <div class="buttons">
      <button @click="$emit('toggle-complete')">Mark as {{ task.completed ? 'Incomplete' : 'Completed' }}</button>
      <button @click="$emit('delete-task')">Delete</button>
    </div>
  </li>
</template>

<script lang="ts" setup>
defineProps({
  task: Object
});

defineEmits(['toggle-complete', 'delete-task']);
</script>

<style scoped>
.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #eee;
  transition: background-color 0.3s;
}

.task-item:hover {
  background-color: #f9f9f9;
}

.completed {
  text-decoration: line-through;
  color: #7f8c8d;
}

.buttons button {
  padding: 5px 10px;
  margin-left: 5px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.buttons button:first-child {
  background-color: #2ecc71;
  color: white;
}

.buttons button:first-child:hover {
  background-color: #27ae60;
}

.buttons button:last-child {
  background-color: #e74c3c;
  color: white;
}

.buttons button:last-child:hover {
  background-color: #c0392b;
}
</style>
