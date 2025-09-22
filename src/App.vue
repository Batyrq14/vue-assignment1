<template>
  <div class="app">
    <h1 class="title">Task Manager</h1>

    <TaskForm @add-task="addTask" />

    <div class="filters">
      <label>Filter by Category:
        <select v-model="filterCategory">
          <option value="">All</option>
          <option value="Work">Work</option>
          <option value="Personal">Personal</option>
          <option value="Shopping">Shopping</option>
        </select>
      </label>

      <label>Filter by Priority:
        <select v-model="filterPriority">
          <option value="">All</option>
          <option value="Low">Low</option>
          <option value="Medium">Medium</option>
          <option value="High">High</option>
        </select>
      </label>

      <label>
        <input type="checkbox" v-model="showIncompleteOnly" />
        Show Incomplete Only
      </label>
    </div>

    <TaskList
      :tasks="filteredTasks"
      :incompleteCount="incompleteCount"
      @toggle-complete="toggleComplete"
      @delete-task="deleteTask"
    />
  </div>
</template>

<script lang="ts" setup>
import { ref, computed } from 'vue';
import TaskForm from './components/TaskForm.vue';
import TaskList from './components/TaskList.vue';

const tasks = ref([]);
const filterCategory = ref('');
const filterPriority = ref('');
const showIncompleteOnly = ref(false);

const addTask = (newTask) => {
  tasks.value.push({
    id: Date.now(),
    text: newTask.text,
    priority: newTask.priority,
    category: newTask.category,
    completed: false
  });
};

const toggleComplete = (id) => {
  const task = tasks.value.find(t => t.id === id);
  if (task) task.completed = !task.completed;
};

const deleteTask = (id) => {
  tasks.value = tasks.value.filter(t => t.id !== id);
};

const incompleteCount = computed(() => {
  return tasks.value.filter(t => !t.completed).length;
});

const filteredTasks = computed(() => {
  return tasks.value.filter(task => {
    const matchesCategory = !filterCategory.value || task.category === filterCategory.value;
    const matchesPriority = !filterPriority.value || task.priority === filterPriority.value;
    const matchesIncomplete = !showIncompleteOnly.value || !task.completed;
    return matchesCategory && matchesPriority && matchesIncomplete;
  });
});
</script>

<style>
.app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
  background-color: #f5f7fa;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.title {
  color: #2c3e50;
  text-align: center;
  margin-bottom: 20px;
}

.filters {
  margin: 20px 0;
  display: flex;
  gap: 15px;
  flex-wrap: wrap;
}

.filters label {
  display: flex;
  align-items: center;
  gap: 5px;
}

.filters select, .filters input[type="checkbox"] {
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
  background-color: #fff;
  transition: border-color 0.3s;
}

.filters select:focus, .filters input[type="checkbox"]:focus {
  border-color: #3498db;
  outline: none;
}
</style>
