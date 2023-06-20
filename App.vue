<template>
    <div>
      <h1>Lista zadań</h1>
      <form @submit.prevent="addTask">
        <input v-model="newTask" type="text" placeholder="Nowe zadanie" required>
        <button type="submit">Dodaj zadanie</button>
      </form>
      <ul>
        <li v-for="(task, index) in tasks" :key="index">
          <span :class="{ completed: task.completed }">{{ task.description }}</span>
          <button @click="deleteTask(index)">Usuń</button>
          <button @click="toggleTaskStatus(index)">
            {{ task.completed ? 'Oznacz jako nieukończone' : 'Oznacz jako ukończone' }}
          </button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        newTask: '',
        tasks: []
      };
    },
    methods: {
      addTask() {
        this.tasks.push({ description: this.newTask, completed: false });
        this.newTask = '';
      },
      deleteTask(index) {
        this.tasks.splice(index, 1);
      },
      toggleTaskStatus(index) {
        this.tasks[index].completed = !this.tasks[index].completed;
      }
    }
  };
  </script>
  
  <style>
  .completed {
    text-decoration: line-through;
  }
  </style>
