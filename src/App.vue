<template>
 <div class="container">
 <Header @toggle-add-task="toggleAddTask" title="Task Tracker!!" :showAddTaskBooleanProp="showAddTask"/>


 <!-- <div v-if="showAddTask"> -->
 <div v-show="showAddTask">
 <AddTask @add-task="addTask"/>
 </div>

 <Tasks 
 @toggle-reminder="toggleReminder"
 @delete-task="deleteTask" :tasks="tasksA"/>
 

 </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
 Header,
 Tasks,
 AddTask
  },
  data() {
    return {
      tasksA: [],
      showAddTask: false
    }
  },
  methods: {
    toggleAddTask(){
       this.showAddTask = !this.showAddTask
    },


     async addTask(t) {

       const res = await fetch('api/tasksA', {
         method: 'POST',
         headers: {
           'Content-type': 'application/json',
         },
         body: JSON.stringify(t)
       })

       const data =  await res.json()
    this.tasksA = [...this.tasksA, data]
  },
    async deleteTask(id) {
      // if (confirm('Sure you wanna do this?')){
      // this.tasksA = this.tasksA.filter((t) => t.id !== id)
      // }

       const res = await fetch(`api/tasksA/${id}`, {
         method: 'DELETE',
       })

       res.status === 200 ? 
       this.tasksA = this.tasksA.filter((t) => t.id !== id) :
       alert('Something went wrong')

  },
  async toggleReminder(id){

const taskToToggle = await this.fetchTask(id)

const updTask = {...taskToToggle, reminder: !taskToToggle.reminder}
console.log(updTask)

const res = await fetch(`api/tasksA/${id}`, {
  method: 'PUT',
  headers: {'Content-type': 'application/json'},
  body: JSON.stringify(updTask)
})

const data = await res.json()

this.tasksA = this.tasksA.map(
  (task) => task.id === id ?
  {...task, reminder: data.reminder} :
  task
)
  },


 async fetchTasks(){
    const res = await fetch('api/tasksA')

    const data = await res.json()
    return data
 },

  async fetchTask(id){
    const res = await fetch(`api/tasksA/${id}`)

    const data = await res.json()
    return data
 }
  
  },
  async created() {
    this.tasksA = await this.fetchTasks()
  }
}
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */

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
