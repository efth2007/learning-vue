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


     addTask(t) {
    this.tasksA = [...this.tasksA, t]
  },
    deleteTask(id) {
      // if (confirm('Sure you wanna do this?')){
      // this.tasksA = this.tasksA.filter((t) => t.id !== id)
      // }

       this.tasksA = this.tasksA.filter((t) => t.id !== id)

  },
  toggleReminder(id){
console.log(`your id: ${id}`)
this.tasksA = this.tasksA.map(
  (task) => task.id === id ?
  {...task, reminder: !task.reminder} :
  task
)
  },
 async fetchTasks(){
    const res = await fetch('http://localhost:3000/tasksA')

    const data = await res.json()
    return data
 },


  
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
