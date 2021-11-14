<template>
  <div class="container">
    <Header />
    <AddTask  @add-task ="addTask"/>
    <Tasks :tasks='tasks' @delete-task="deleteTask" @toggle-reminder="toggleReminder" /> 
    
  </div>
  
  
</template>

<script>
import Header from './components/Header'
import AddTask from './components/AddTask'
import Tasks from './components/Tasks'

export default {
  name: 'App',
  data(){
    return{
      tasks: []
    }
  },
  methods:{
    deleteTask(id){
      if(confirm('Are you sure?')) {
        this.tasks = this.tasks.filter((task)=> task.id !== id);
      }
    },
    toggleReminder(id){
      this.tasks = this.tasks.map((task)=> task.id === id ? {...task, reminder:!task.reminder} : task);
    },
    addTask(task){
      this.tasks = [ ...this.tasks , task ];
    }
  },
  created(){
    this.tasks =  [
        {
          id:1,
          text: 'First Task',
          day:'20 march 2022',
          reminder: true

        },
        {
          id:2,
          text: 'Second Task',
          day:'20 march 2022',
          reminder: false

        },
        {
          id:3,
          text: 'Third Task',
          day:'20 march 2022',
          reminder: false
        },
      ]
  },
  components: {
    Header,
    Tasks,
    AddTask
  },
  emits:[''],
}
</script>

<style>
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
