<template>
    <div class="todo-content">
        <h1>Todo-list</h1>
        <HeaderTodo @createTodo="handleCreateTodo"/>
        <BodyTodo 
            :data="data" 
            @delete-todo="handleDeleteTodo" 
            @confirm-todo="handleConfirmTodo"   
            @settings-todo="handleEditTodo"
        />
    </div>
</template>

<script setup>
    import HeaderTodo from './header-todo.vue';
    import BodyTodo from './body-todo.vue';
    import { ref } from 'vue';

    const data = ref([
        { id: 1, description: 'agendamento 1', flag: 1},
        { id: 2, description: 'agendamento 2', flag: 0},
        { id: 3, description: 'agendamento 3', flag: 0},
        { id: 4, description: 'agendamento 4', flag: 0}
    ]);

    const handleCreateTodo = (todo) => {
        data.value.find((el => el.description === todo)) ? 
            alert('Tarefa já existe!') : 
            data.value.push({id: 5, description: todo})
    }

    const handleDeleteTodo = (row) => {
        const newData = data.value.findIndex((el) => el.id === row.id) 
        data.value.splice(newData, 1)
    }

    const handleConfirmTodo = (row) => {
        const el = data.value.findIndex((el) => el.id === row.id) 
        data.value[el].flag = !row.flag; 
    }

    const handleEditTodo = (row) => {
        const el = data.value.findIndex((el) => el.id === row.id) 
        data.value[el].description = row.description; 
    }
</script>

<style scoped>
    .todo-content {
        padding: 50px;
        display: flex;
        flex-direction: column;
        align-items: center;
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        border-radius: 20px;
        width: 1000px;
        min-height: 500px;
        gap: 20px;
        box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
    }

    .todo-content h1 {
        color: white;
        font-size: 2.5rem;
        font-weight: 700;
        margin: 0;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
        letter-spacing: 1px;
    }
</style>