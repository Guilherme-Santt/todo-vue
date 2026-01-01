<template>
    <div class="todo-content">
        <h1>Todo-list</h1>
        <HeaderTodo />
        <BodyTodo />
    </div>
</template>

<script setup>
    import HeaderTodo from './header-todo.vue';
    import BodyTodo from './body-todo.vue';
</script>

<style scoped>
    .todo-content {
        padding: 50px;
        display: flex;
        flex-direction: column;
        align-items: center;
        background-color: rgb(151, 83, 240);
        border-radius: 10px;
        width: 1000px;
        height: 500px;
    }
</style>