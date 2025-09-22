<template>
  <div class="task-list">
    <p class="count">Incomplete Tasks: {{ incompleteCount }}</p>

    <ul v-if="tasks.length > 0" class="task-items">
      <TaskItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @toggle-complete="$emit('toggle-complete', task.id)"
        @delete-task="$emit('delete-task', task.id)"
      />
    </ul>

    <p v-else class="no-tasks">No tasks</p>
  </div>
</template>

<script lang="ts" setup>
import TaskItem from './TaskItem.vue';

defineProps({
  tasks: Array,
  incompleteCount: Number
});

defineEmits(['toggle-complete', 'delete-task']);
</script>

<style scoped>
.task-list {
  background-color: #fff;
  padding: 15px;
  border-radius: 4px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.count {
  font-weight: bold;
  color: #2c3e50;
  margin-bottom: 10px;
}

.task-items {
  list-style: none;
  padding: 0;
}

.no-tasks {
  color: #7f8c8d;
  text-align: center;
}
</style>
