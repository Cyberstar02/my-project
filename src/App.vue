<template>
  <div id="app">
    <h1>My To-Do List</h1>

    <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task" />
    <button @click="addTask">Add</button>

    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <span :style="{ textDecoration: task.done ? 'line-through' : 'none' }">
          {{ task.text }}
        </span>
        <button @click="toggleDone(index)">✅</button>
        <button @click="removeTask(index)">❌</button>
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

input {
  padding: 8px;
  width: 65%;
  margin-right: 10px;
}

button {
  margin-left: 5px;
  padding: 5px 10px;
  cursor: pointer;
}

li {
  margin: 10px 0;
  list-style: none;
}
</style>
