<script setup>
import Task from './Task.vue';
</script>

<template>
    <div :key="task.id" v-for="task in tasks">
        <Task @delete-task="$emit('delete-task', task.id)" :task="task" />
    </div>
</template>

<script>
    export default {
        name: 'Tasks',
        props: {
            tasks: Array
        },
    emits: ['delete-task'],
    }
</script>