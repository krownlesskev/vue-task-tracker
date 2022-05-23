<template>
    <div class="task">
        <h3>{{task.text}}
            <p class="delete-btn">x</p>
        </h3>
        <p>{{task.day}}</p>
    </div>
</template>

<script>
export default {
    name: "Task",
    props: {
        task: Object
    }
}

</script>


<style scope>
.task {
    background-color: #777;
    margin: .5rem 0;
    padding: .5rem;
    color: #fff;
    transition: .3s;
}

.task.reminder {
    border-left: 2px solid yellow;
}

h3 {
    display: flex;
    justify-content: space-between;
}

.delete-btn {
    margin-right: 2rem;
    background-color: red;
    border-radius: 10px;
    padding: 0 10px;
    transition: .3s;
}

.delete-btn:hover {
    cursor: pointer;
    transform: scale(1.25);
    transition: .3s;
}
</style>