<template>
    <div class="todo-content">
        <h1>Todo-list</h1>
        <HeaderTodo @createTodo="handleCreateTodo"/>
        <BodyTodo 
            :data="data" 
            @delete-todo="handleDeleteTodo" 
            @confirm-todo="handleConfirmTodo"   
            @settings-todo="handleEditTodo"
            @clean-all-todo="data = [] && notificar('success', 'Todas as tarefas foram removidas com sucesso!')"
        />
    </div>
</template>

<script setup>
    import HeaderTodo from './header-todo.vue';
    import BodyTodo from './body-todo.vue';
    import { ref } from 'vue';
    import Swal from 'sweetalert2'

    const Toast = Swal.mixin({
        toast: true,
        position: 'top-end',
        showConfirmButton: false,
        timer: 3000,
        timerProgressBar: true,
        didOpen: (toast) => {
            toast.onmouseenter = Swal.stopTimer;
            toast.onmouseleave = Swal.resumeTimer;
        }
    })

    const notificar = (icon, message) => {
        Toast.fire({
            icon: icon || 'success',
            title: message || 'Tarefa adicionada com sucesso!'
        })
    }

    const data = ref([
        { id: 1, description: 'agendamento 1', flag: 1},
        { id: 2, description: 'agendamento 2', flag: 0},
        { id: 3, description: 'agendamento 3', flag: 0},
        { id: 4, description: 'agendamento 4', flag: 0}
    ]);

    const handleCreateTodo = (todo) => {
        if(todo === '') {
            return notificar('error', 'Digite uma tarefa válida!')
        }
        
        data.value.find((el => el.description === todo)) ? 
            notificar('error', 'Tarefa já existe!') : 
            data.value.push({id: 5, description: todo}) && notificar('success', 'Tarefa adicionada com sucesso!')   
    }

    const handleDeleteTodo = (row) => {
        const newData = data.value.findIndex((el) => el.id === row.id) 
        data.value.splice(newData, 1)

        notificar('success', 'Tarefa removida com sucesso!')
    }

    const handleConfirmTodo = (row) => {
        const el = data.value.findIndex((el) => el.id === row.id) 
        data.value[el].flag = !row.flag; 

        notificar('success', 'Tarefa atualizada com sucesso!')
    }

    const handleEditTodo = (row) => {
        const el = data.value.findIndex((el) => el.id === row.id) 
        data.value[el].description = row.description; 

        notificar('success', 'Tarefa editada com sucesso!')
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