<template>
  <div>
    <p>Incomplete Tasks: {{ incompleteCount }}</p>

    <ul v-if="tasks.length > 0">
      <TaskItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @toggle-complete="$emit('toggle-complete', task.id)"
        @delete-task="$emit('delete-task', task.id)"
      />
    </ul>

    <p v-else>No tasks</p>
  </div>
</template>

<script setup>
import TaskItem from './TaskItem.vue';

defineProps({
  tasks: Array,
  incompleteCount: Number
});

defineEmits(['toggle-complete', 'delete-task']);
</script>

<style scoped>
ul { list-style: none; padding: 0; }
</style>
