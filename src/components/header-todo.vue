<template>
    <header :class="['header-content']">
        <input :class="['input-content']" type="text" name="" id="" placeholder="Digite a tarefa...">
        <button :class="['btn-content']">+</button>
    </header>
</template>

<script setup>
  // Lógica do cabeçalho (se houver)
</script>

<style scoped>
    .header-content { 
        border: 1px solid #e6e6e6; 
        background-color: white; 
        border-radius: 10px; 
        padding: 20px 10px; 
        width: 490px;
        display: flex;
        column-gap: 10px;
        align-items: start;
    }
    
    .input-content { 
        border: none; 
        width: 400px; 
        border: 1px solid #e6e6e6; 
        background-color: white; 
        border-radius: 5px; 
        padding: 10px; 
    }

    .input-content:hover {
        box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px; 
        transition: 0.3s all;
        cursor: pointer;
    }

    .input-content:focus {
        border: 1px solid #8100cc !important;
    }
    
    .btn-content {
        cursor: pointer;
        background-color: #8100cc;
        border: none;
        color: white;
        padding: 10px 20px;
        border-radius: 10px;
        transition: transform 0.3s ease; 
    }
    .btn-content:hover {
        transform: scale(1.2);
    }
</style>    