<template>
  <div class="container">
    <Header title ="Task Tracker" @toggle-add-task="toggleAddTask" :showAddTask="showAddTask" />
    <div v-show="showAddTask">
      <AddTask @add-task ="addTask"/>
    </div>
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
      tasks: [],
      showAddTask : false,
    }
  },
  methods:{
    async deleteTask(id){
      if(confirm('Are you sure?')) {
        const res = await fetch(`api/tasks/${id}`, {
          method:'DELETE',
          headers:{
            'Content-type': 'application/json'
          }
        });
        res.status === 200 ? this.tasks = this.tasks.filter((task)=> task.id !== id) : alert('ERROR DELETING TASK');
      
      }
    },
    async toggleReminder(id){
      const taskToToggle = await this.fetchTask(id);
      const updTask = {...taskToToggle , reminder: !taskToToggle.reminder};
      const res = await fetch(`api/tasks/${id}`, {
          method:'PUT',
          headers:{
            'Content-type': 'application/json'
          },
          body: JSON.stringify(updTask)
        });
        const data = await res.json();
        //console.log(data);
      this.tasks = this.tasks.map((task)=> task.id === id ? {...task, reminder:data.reminder} : task);
    },
    async addTask(task){
      //const newTasks = [...data , task];
      //console.log(newTasks);
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers:{
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task)
      });
      const data = await res.json();
      this.tasks = [ ...this.tasks , data ];
    },
    toggleAddTask(){
      this.showAddTask = !this.showAddTask;
    },
    async fetchTasks(){
      const res = await fetch('api/tasks');
      const data = await res.json();
      return data;
    },
    async fetchTask(id){
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    }
  },
  async created(){
    this.tasks = await this.fetchTasks();
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
