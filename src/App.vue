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
      background: linear-gradient(135deg, #e0c3fc 0%, #8ec5fc 100%);
      width: 100vw;
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      position: relative;
      overflow: hidden;
  }

  .container::before {
      content: '';
      position: absolute;
      width: 500px;
      height: 500px;
      background: radial-gradient(circle, rgba(102, 126, 234, 0.1) 0%, transparent 70%);
      top: -150px;
      left: -150px;
      animation: float 6s ease-in-out infinite;
  }

  .container::after {
      content: '';
      position: absolute;
      width: 400px;
      height: 400px;
      background: radial-gradient(circle, rgba(118, 75, 162, 0.1) 0%, transparent 70%);
      bottom: -100px;
      right: -100px;
      animation: float 8s ease-in-out infinite reverse;
  }

  @keyframes float {
      0%, 100% {
          transform: translateY(0) rotate(0deg);
      }
      50% {
          transform: translateY(-20px) rotate(5deg);
      }
  }
</style>
