
<template>
  <div :class="['container']">
    <Todo />
  </div>
</template>

<script setup>
  import Todo from './components/todo.vue';

</script>

<style scoped>
  .container {
    background-color: white !important;
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  } 
</style>