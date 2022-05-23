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


   async addTask(task) {
     const res = await fetch('api/tasks', {
       method: 'POST',
       headers: {
         'Content-type': 'application/json',
         
       },
       body: JSON.stringify(task)
     })
     
      const data = await res.json()

      this.tasks = [...this.tasks, data]
    },


    async deleteTask(id) {
      if(confirm('Are you sure?')) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE',

        })

        res.status === 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id)) : alert('Error Deleting Task')
        
      }
    },


    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id)
      const updateTask = {...taskToToggle, reminder: !taskToToggle.reminder}

      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type' : 'application/json'
        },
        body: JSON.stringify(updateTask)
      })

      const data = await res.json()

      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: data.reminder} : task)
    },


    async fetchTasks() {
      const res = await fetch('api/tasks')
      const data = await res.json()

      return data
    },


    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`)
      const data = await res.json()

      return data
    },

  },  
  
  async created() {
    this.tasks = await this.fetchTasks()
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
