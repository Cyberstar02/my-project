<template>
  <div id="app">
    <h1>My To-Do List</h1>

    <!-- Input and Add button -->
    <n-input
      v-model:value="newTask"
      placeholder="Add a new task"
      style="width: 65%; margin-right: 10px"
      @keyup.enter="addTask"
    />
    <n-button type="primary" @click="addTask">Add</n-button>

    <!-- Task List -->
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <span :style="{ textDecoration: task.done ? 'line-through' : 'none' }">
          {{ task.text }}
        </span>
        <n-button
          size="small"
          type="success"
          tertiary
          style="margin-left: 5px"
          @click="toggleDone(index)"
        >✅</n-button>
        <n-button
          size="small"
          type="error"
          tertiary
          style="margin-left: 5px"
          @click="removeTask(index)"
        >❌</n-button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      newTask: '',
      tasks: []
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ text: this.newTask, done: false });
        this.newTask = '';
      }
    },
    toggleDone(index) {
      this.tasks[index].done = !this.tasks[index].done;
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  padding: 30px;
  max-width: 500px;
  margin: auto;
  text-align: center;
}

ul {
  padding: 0;
}

li {
  margin: 10px 0;
  list-style: none;
}
</style>