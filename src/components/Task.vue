<template>
    <div @dblclick="$emit('toggle-reminder',task.id)" :class="[task.reminder? 'reminder' : '' , 'task']">
        <h3>{{ task.text }}
            <i @click="onDelete(task.id)" class="fas fa-times"></i>
        </h3>
        <p>{{ task.day }}</p>
    </div>
    
</template>
<script>
export default {
    name:'Task',
    props: {
        task : Object,
    },
    methods:{
        onDelete(id){
            this.$emit('delete-task' , id)
        }
    }
}
</script>
<style scoped>
.task-item{
    padding: 10px 2px;
}
.reminder{
    border-left: 3px solid green;
}
.fas{
   color: red; 
}
</style>