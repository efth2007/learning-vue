<template>
    <header>
        <h1>{{title}}</h1>
         <Button @btn-click="$emit('toggle-add-task')" 
         :text="showAddTaskBooleanProp ? 'Hide form' : 'Add Task!'" 
         :color="showAddTaskBooleanProp ? 'red' : 'blue'"/>

    </header>
</template>

<script>
import Button from './Button.vue'

export default {
    name: 'Header',
    props: ['title', 'showAddTaskBooleanProp'],
    components: {
        Button
    }
}
</script>



// "scoped" means that this style below is only gonna be used for this component
<style scoped> 
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}

</style>