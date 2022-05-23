<script setup>
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue';
</script>

<template>
  <div class="container">
    <Header  title="Task Tracker"/>
    <Tasks :tasks="tasks"/>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      tasks: []
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Appointment',
        day: 'March 1st at 2:30pm',
        reminder: true,
      },
      {
        id: 2,
        text: 'Meeting at School',
        day: 'March 3rd at 1:30pm',
        reminder: true,
      },
      {
        id: 3,
        text: 'Food Shopping',
        day: 'March 4th at 11:00am',
        reminder: false,
      },
    ]
  }
}

</script>

<style>
@import './assets/base.css';

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  border: 1px solid red;
  padding: 1rem;
  width: 500px;
}

.btn {
  padding: 10px;
  border: none;
  border-radius: 10px;
  transition: .3s;
}

.btn:hover {
  cursor: pointer;
  transform: scale(1.1);
  transition: .3s;
}
</style>
