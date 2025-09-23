<template>
  <form @submit.prevent="handleSubmit" class="task-form">
    <input
      v-model="text"
      type="text"
      placeholder="Enter task text"
      required
    />

    <select v-model="priority" required>
      <option value="" disabled>Select Priority</option>
      <option value="Low">Low</option>
      <option value="Medium">Medium</option>
      <option value="High">High</option>
    </select>

    <select v-model="category" required>
      <option value="" disabled>Select Category</option>
      <option value="Work">Work</option>
      <option value="Personal">Personal</option>
      <option value="Shopping">Shopping</option>
    </select>

    <button type="submit">Add Task</button>
  </form>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

const text = ref('');
const priority = ref('');
const category = ref('');

const emit = defineEmits(['add-task']);

const handleSubmit = () => {
  if (text.value && priority.value && category.value) {
    emit('add-task', { text: text.value, priority: priority.value, category: category.value });
    text.value = '';
    priority.value = '';
    category.value = '';
  }
};
</script>

<style scoped>
.task-form {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.task-form input, .task-form select, .task-form button {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 14px;
}

.task-form input:focus, .task-form select:focus {
  border-color: #3498db;
  outline: none;
}

.task-form button {
  background-color: #3498db;
  color: white;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s;
}

.task-form button:hover {
  background-color: #2980b9;
}
</style>
