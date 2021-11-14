<template>
    <div class="tasks">
        <div v-for="task in tasks" :key="task.id">
            <Task :task = 'task' @delete-task = "$emit('delete-task',task.id)" @toggle-reminder="$emit('toggle-reminder',task.id)"/>
        </div>
    </div>
</template>

<script>
import Task from './Task'
export default{
    name: 'Tasks',
    components: {
        Task,
    },
    
    props: ['tasks'],
    emits:['delete-task', 'toggle-reminder']
}
</script>



<style scope>
.task{
    margin:5px;
    padding: 10px 20px;
    background-color: #f4f4f4;
    cursor: pointer;
}

.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>