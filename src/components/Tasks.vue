<template>
  <!-- Looping through the tasks and output task-->
  <div :key="task.id" v-for="task in tasks">
    <!-- There was an error poppe out asking for an ID, so the key was added-->
    <!-- We catch the emit from the lower children component Task-->
    <Task
      @toggle-completed="$emit('toggle-completed', task.id)"
      @delete-task="$emit('delete-task', task.id)"
      :task="task"
    />
    <!--We emit 'detete' one up level to App.vue-->
  </div>
</template>

<script>
import Task from './Task';
export default {
  name: 'Tasks',
  props: {
    tasks: Array,
  },
  components: {
    Task,
  },
  //emits added here because there was an error came out saying that "emits event Listeners were passed to component but could not be automatically inherited...".
  emits: ['delete-task', 'toggle-completed'],
};
</script>
