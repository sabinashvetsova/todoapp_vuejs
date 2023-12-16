<template>
  <h1>TODO list</h1>
  <ul>
    <li v-for="(task, index) in tasksToShow" :key="task">
      <input type="checkbox" @click="completeTask(task)" />{{ task }}
      <button type="button" @click="deleteTask(index, task)">x</button>
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
export default {
  data() {
    return {
      tasks: ["Wash the car", "Feed the dog", "Make dinner"],
      newTask: "",
      completedTasks: [],
      showCompletedTasks: false,
    };
  },
  methods: {
    addNewTask() {
      this.tasks.push(this.newTask);
      this.newTask = "";
    },
    deleteTask(index, task) {
      this.tasks.splice(index, 1);
      index = this.completedTasks.indexOf(task);
      if (index > -1) {
        this.completedTasks.splice(index, 1);
      }
    },
    completeTask(task) {
      const index = this.completedTasks.indexOf(task);
      if (index > -1) {
        this.completedTasks.splice(index, 1);
      } else this.completedTasks.push(task);
    },
  },
  computed: {
    tasksToShow() {
      return this.showCompletedTasks ? this.completedTasks : this.tasks;
    },
    buttonMessage() {
      return this.showCompletedTasks
        ? "Show all tasks"
        : "Show completed tasks";
    },
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
