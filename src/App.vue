<template>
  <div id="app">
    <div class="container">
      <Header :showAddTask = "showAddTask" @show-form="showTask" title = 'Task Tracker'/>
      <div v-show="showAddTask">
        <addTask @add-task="addingTask"/>
      </div>
      <Tasks @toggle-reminder = "toggleReminder" @delete-task="deleteTask" v-bind:tasks = "tasks"/>
    </div>
    
  </div>
</template>

<script>
import addTask from './components/addTask'
import Header from './components/Header'
import Tasks from './components/Tasks'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    addTask,
    
  },
  data() {
    return{
      tasks:[],
      showAddTask:false
      }
  },
  methods: {
    deleteTask(id){
      if(confirm('Are you sure?')){
        this.tasks = this.tasks.filter((task)=> task.id !== id)
      }
    },
    toggleReminder(id){
      this.tasks = this.tasks.map((task)=>task.id === id ? {...task, reminder: !task.reminder} : task)
    },
    addingTask(newTask){
      this.tasks = [...this.tasks, newTask]
    },
    showTask(){
      this.showAddTask = !this.showAddTask
    }
  },
  created(){
    this.tasks = [
      {
        id:1,
        text: 'pierwsze',
        day:"iabdai",
        reminder:true,
      },
      {
        id:2,
        text:"drugie",
        day:"dadafae",
        reminder:false,
      }
    ]
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
