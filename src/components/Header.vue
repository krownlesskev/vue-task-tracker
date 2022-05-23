<script setup>
import Button from './Button.vue';
</script>


<template>
    <header>
        <h1>{{title}}</h1>
        <Button @click="onClick()" text="Add Task" color="#fff"/>
    </header>
</template>

<script>
    export default {
        name: 'Header',
        props: {
            title: String,
        },
        components: {
            Button
        },
        methods: {
            onClick() {
                console.log('click')
            }
        }
    }
</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>