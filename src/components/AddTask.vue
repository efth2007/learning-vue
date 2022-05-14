<template>
   <form @submit="onSubmit" clas="add-form">
        <div class="form-control">
            <label>Task</label>
            <input type="text" v-model="text" name="text" placeholder="Text here!">
        </div>
           <div class="form-control">
            <label>Date</label>
            <input type="text" v-model="day" name="day" placeholder="Date here!">
        </div>
           <div class="form-control">
            <label>Set reminder</label>
            <input type="checkbox" v-model="reminder" name="reminder">
        </div>
        <input class="btn btn-block" type="submit" value="Save Task"/>
    </form>
    
</template>

<script>
export default {
    name: 'AddTask',
    data(){
        return {
            text:'poiuytre',
            day:'',
            reminder: false
        }
    },
    methods:{
        onSubmit(e){
            e.preventDefault()
            
            if (!this.text){
                alert('Nothing typed...')
                return
            }

            const newTask = {
               // id: Math.floor(Math.random() * 10000),
                text: this.text,
                day: this.day,
                reminder: this.reminder
            }


this.text=""
this.day=""
this.reminder= false


            this.$emit('add-task', newTask)
        }
    }
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>