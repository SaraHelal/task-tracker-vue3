<template>
    <div class="header">
        <h1>{{title}}</h1>
        <Button :color ="showAddTask? 'red' : 'green'" :text= "showAddTask? 'Close' : 'Add Task'" @btn-click="$emit('toggle-add-task')" />
    </div>
</template>

<script>
import Button from './Button'
export default{
    name: 'Header',
    components: { Button },
    props:{
        title: String,
        showAddTask : Boolean,
    },
    emits: ['toggle-add-task'],
}
</script>



<style scoped>
.header {
    display: flex;
    justify-content: space-between;
}
</style>