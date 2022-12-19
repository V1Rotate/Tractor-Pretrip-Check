<template>
  <!-- if a task is completed, we are asking if the task 'completed' status is 'true', this div needs to have class 'completed', so this exact task will have a left green bar\border maeking this task indicated as completed. Otherwise, set class 'task' as others which are not indicated as completed.-->

  <div
    @click="$emit('toggle-completed', task.id)"
    :class="[
      task.completed
        ? 'border-solid border-green-600 border-l-4  duration-200 font-thin'
        : '',
      'my-4 py-1 px-2 rounded-sm cursor-pointer bg-gray-100 font-medium',
    ]"
  >
    <h3 class="flex items-center justify-between">
      {{ task.text }}
      <!-- 'i' is task delete icon in case a task is not aplicable to the specific truck--><i
        @click="$emit('delete-task', task.id)"
        class="fas fa-times"
      ></i>
    </h3>
  </div>
</template>

<script>
export default {
  name: 'Task',
  props: {
    task: Object,
  },
};
</script>

<!--Font-awesome nice remove symbol applied only.-->
<style scoped>
.fas {
  color: red;
}
</style>
