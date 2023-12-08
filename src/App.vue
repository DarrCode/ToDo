<script setup lang="ts">
import TodoList from "./components/TodoList.vue";
</script>

<template>
  <div class="card">
    <h1>ToDo App</h1>

    <div class="card-body">
      <TodoList />
    </div>
  </div>
</template>

<style lang="scss" scoped>
$color-fondo: #f2f2f2;
$padding-interior: 20px;
$border-radius: 15px;
$sombra: 0 2px 4px rgba(0, 0, 0, 0.1); // Definir la sombra
.card {
  background-color: $color-fondo;
  padding: $padding-interior;
  border-radius: $border-radius;
  display: flex;
  flex-direction: column;
  align-items: center;
  box-shadow: $sombra; // Agregar la sombra

  h1 {
    color: #1a1a1a;
    font-size: 34px;
    margin-bottom: 20px;
  }
}
</style>
