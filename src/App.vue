<script setup>
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue';
import AddTask from './components/AddTask.vue';
</script>

<template>
  <div class="container">
    <Header 
    @toggle-add-task="toggleAddTask"  
    title="Task Tracker"
    :showAddTask="showAddTask"
    />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask"/>
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      tasks: [],
      showAddTask: false,
    }
  },

  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id) {
      if(confirm('Are you sure?')) {
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: !task.reminder} : task)
    },
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
  border-radius: 20px;
  padding: 1rem;
  width: 500px;
  background-image: linear-gradient(to bottom right, #003170, rgb(0, 0, 0));
  box-shadow: 5px 5px 20px #000;
}

.btn {
  padding: 10px;
  border: none;
  border-radius: 10px;
  transition: .3s;
}

.btn-block {
  width: 100%;
}

.btn:hover {
  cursor: pointer;
  transform: scale(1.1);
  transition: .3s;
}
</style>
