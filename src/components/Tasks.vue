<template>
    <div v-for="task in tasks" :key="task.id" >
        <!-- <h3>{{task.text}}</h3> -->
        <Task 
        @toggle-reminder="$emit('toggle-reminder', task.id)"
        @delete-task="$emit('delete-task', task.id)" :task="task"/>
    </div>
</template>

<script>
import Task from './Task.vue'

export default {
    name: 'Tasks',
    //two different ways to define props: 
    //the one below and the one as in the 'Header' coponent
    props: {
        tasks: Array
    },


    components: {
        Task
    },
    emits: ['delete-task', 'toggle-reminder']

}
</script>