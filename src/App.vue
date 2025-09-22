<template>
  <div class="app">
    <h1>Task Manager</h1>

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
.app { max-width: 600px; margin: 0 auto; padding: 20px; }
.filters { margin: 20px 0; display: flex; gap: 10px; flex-wrap: wrap; }
</style>
