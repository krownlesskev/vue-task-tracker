<template>
    <div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
        <h3>{{task.text}}
            <p @click="$emit('delete-task', task.id)" class="delete-btn">x</p>
        </h3>
        <p>{{task.day}}</p>
    </div>
</template>

<script>
export default {
    name: "Task",
    props: {
        task: Object,
    }
}


</script>


<style>
.task {
    background-color: #777;
    margin: .5rem 0;
    padding: .5rem;
    color: #fff;
    transition: .3s;
    
}

.task.reminder {
    border-left: 5px solid #fff;
}

h3 {
    display: flex;
    justify-content: space-between;
}

.delete-btn {
    margin-right: 2rem;
    color: red;
    font-size: 24px;
    font-weight: 600;
    border-radius: 10px;
    padding: 0 10px;
    transition: .3s;
}

.delete-btn:hover {
    cursor: pointer;
    transform: scale(1.5);
    transition: .3s;
}
</style>