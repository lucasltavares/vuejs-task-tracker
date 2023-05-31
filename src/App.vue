<template>
  <div class="container">
    <Header 
    @toggle-add-task="toggleAddTask()"
    title="Task Tracker" 
    :showAddTask="showAddTask" />
    <div v-show="showAddTask">
      <addTask @add-task="addTask" />
    </div>
    <Tasks 
    @toggle-reminder="toggleReminder" 
    @delete-task="deleteTask" 
    :tasks="tasks" />
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Header from './components/header.vue'
import Tasks from './components/tasks.vue'
import addTask from './components/addTask.vue'
export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    addTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    }
  },
  methods: {
    deleteTask(id) {
      if(confirm('Are you sure?')) {
        this.tasks = this.tasks.filter(function deletetask(task) {
        return task.id !== id
        })
      }
    },

    toggleReminder(id) {
      this.tasks = this.tasks.map((task) => task.id === id
        ? {...task, reminder: !task.reminder} : task // Ternary else if.
        )
    },

    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
      console.log(this.showAddTask)
    }
  },
  created() {
    this.tasks = [
    {
      id: 1,
      text: 'Doctor appointment',
      day: 'March 1st',
      reminder: true,
    },
    {
      id: 2,
      text: 'Meeting at School',
      day: 'March 3rd',
      reminder: false
    },
    {
      id: 3,
      text: 'Destroy capitalism',
      day: 'Everyday',
      reminder: true
    }]
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
