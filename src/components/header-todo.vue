
<!-- header-todo.vue -->
<template>
    <header :class="['header-content']">
        <input :class="['input-content']" type="text" name="" id="" placeholder="Digite a tarefa..." v-model="inputCreate">
        <button @click="emit('createTodo', inputCreate)" :class="['btn-content']">+</button>
    </header>
</template>

<script setup>
    import { ref } from 'vue';
    const emit = defineEmits('createTodo')
    const inputCreate = ref('')

</script>

<style scoped>
    .header-content { 
        border: none;
        background: rgba(255, 255, 255, 0.95);
        backdrop-filter: blur(10px);
        border-radius: 15px;
        padding: 15px;
        width: 490px;
        display: flex;
        column-gap: 12px;
        align-items: center;
        box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
    }

    .input-content { 
        border: 2px solid transparent;
        width: 400px;
        background-color: #f8f9fa;
        border-radius: 10px;
        padding: 12px 16px;
        font-size: 15px;
        transition: all 0.3s ease;
        outline: none;
    }

    .input-content:hover {
        background-color: white;
        box-shadow: 0 4px 12px rgba(102, 126, 234, 0.15);
    }

    .input-content:focus {
        border: 2px solid #667eea;
        background-color: white;
        box-shadow: 0 4px 16px rgba(102, 126, 234, 0.25);
    }

    .btn-content {
        cursor: pointer;
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        border: none;
        color: white;
        padding: 12px 24px;
        border-radius: 10px;
        font-size: 20px;
        font-weight: bold;
        transition: all 0.3s ease;
        box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
    }

    .btn-content:hover {
        transform: translateY(-2px);
        box-shadow: 0 6px 20px rgba(102, 126, 234, 0.6);
    }

    .btn-content:active {
        transform: translateY(0);
    }
</style>