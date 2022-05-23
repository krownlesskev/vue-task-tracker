<script setup>
import Task from './Task.vue';
</script>

<template>
    <div :key="task.id" v-for="task in tasks">
        <Task :task="task" />
    </div>
</template>

<script>
    export default {
        name: 'Tasks',
        props: {
            tasks: Array
        }
    }
</script>