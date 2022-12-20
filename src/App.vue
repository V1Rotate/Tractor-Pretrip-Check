<template>
  <div
    class="box-border m-0 font-sans max-w-md bg-white rounded-md p-7 border-2 border-gray-200 overflow-auto mx-auto mt-5"
  >
    <img
      class="max-w-xs my-0 mx-auto"
      src="./assets/truckImg.png"
      alt="Freightliner Cascadia truck"
    />

    <Header
      truckModel="FREIGHTLINER CASCADIA"
      appName="DRIVER'S PRE-TRIP CHECK-LIST* :"
    />

    <!--methods to be created in the methods object section below-->
    <!--toggle-completed is regarding the driver should toggle each point once it is checked and he can delete the check point task if it is not applicable to his truck for some reason to not to confuse him later once he runs thought the whole list.-->
    <Tasks
      @toggle-completed="toggleCompleted"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
    <p class="text-sm text-red-600 text-center mt-8 motion-safe:animate-bounce">
      * With any questions, contact your Shop Supervisor.
    </p>
  </div>
</template>

<script>
import Header from './components/Header'; //Importing the application header with the truck image, truck model and link to the Driver's manual.
import Tasks from './components/Tasks'; //Importing the list of tasks for the driver for the truck pre-trip checking.

export default {
  name: 'App',
  components: { Header, Tasks },
  data() {
    return {
      tasks: [],
    };
  },

  methods: {
    //Registering the delete task here:
    deleteTask(id) {
      //we are not taking the id which was passed here.
      if (
        confirm(
          'Are you sure that this check-point is not applicable to your Freightliner? If so, click "OK". Have a safe trip! '
        )
      ) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    }, //we accept everything back except the task with the id we are looking\filtering for.
    toggleCompleted(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, completed: !task.completed } : task
      ); //we updating tasks by chaning 'completed' (driver's task) to true or false. We map trought the tasks and we return array of updated tasks. We are checking that , of each task, if the task has id equal to the id that passed in. If it is, we return an array of object wher ewe have the innitial tasks and we change our reminder (that green bar ot what ever is opposite to the current task completion status) => true to false and vice versa. In case, it does not match anything, we keep the the completion status the same, false or true.
    },
    //fetching our check-list tasks from the MockAPI.
    async fetchTasks() {
      const res = await fetch(
        'https://639f53405eb8889197fa4891.mockapi.io/tasks/'
      );
      const data = await res.json();
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(
        `https://639f53405eb8889197fa4891.mockapi.io/tasks/${id}`
      );
      const data = await res.json();
      return data;
    },
  },
  //tasks are defined above as an empty array, but we get the access to tasks by fetching them from the MockAPI.

  async created() {
    this.tasks = await this.fetchTasks();
  },
  //!Was thinking to add a Skeleton plugin to show a figures of the tasks in the list, however, I see that fetching from the MockAPI is so fast, so normally there would be not much reason to make the code heavier adding a Skeketion if its not going to be visible to the user. Otherwise, Skeleton may be added.
};
</script>
