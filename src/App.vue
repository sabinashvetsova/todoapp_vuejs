<template>
  <h1>TODO list</h1>
  <ul>
    <li v-for="task in tasksToShow" :key="task">
      <input type="checkbox" @click="completeTask(task)" />{{ task }}
      <button type="button" @click="deleteTask(task)">x</button>
    </li>
  </ul>
  <div>
    <input type="text" v-model="newTask" />
    <button type="button" @click="addNewTask">Add new task</button>
  </div>
  <button type="button" @click="showCompletedTasks = !showCompletedTasks">
    {{ buttonMessage }}
  </button>
</template>

<script>
import { ref, computed } from "vue";
export default {
  name: "App",
  setup() {
    const tasks = ref(["Wash the car", "Feed the dog", "Make dinner"]);
    const newTask = ref("");
    const showCompletedTasks = ref(false);

    const buttonMessage = computed(() => {
      return showCompletedTasks.value
        ? "Show all tasks"
        : "Show completed tasks";
    });

    const completedTasks = ref([]);

    function completeTask(task) {
      const index = completedTasks.value.indexOf(task);
      if (index > -1) {
        completedTasks.value.splice(index, 1);
      } else completedTasks.value.push(task);
    }

    const tasksToShow = computed(() => {
      return showCompletedTasks.value ? completedTasks.value : tasks.value;
    });

    function addNewTask() {
      tasks.value.push(newTask.value);
      newTask.value = "";
    }

    function deleteTask(task) {
      let index = tasks.value.indexOf(task);
      tasks.value.splice(index, 1);

      index = completedTasks.value.indexOf(task);
      console.log(index);
      if (index > -1) {
        completedTasks.value.splice(index, 1);
      }
    }

    return {
      tasks,
      newTask,
      buttonMessage,
      completeTask,
      showCompletedTasks,
      tasksToShow,
      addNewTask,
      deleteTask,
    };
  },
};
</script>

<style scoped>
ul {
  /* margin: 0; */
  list-style: none;
  /* float: left; */
}
</style>
