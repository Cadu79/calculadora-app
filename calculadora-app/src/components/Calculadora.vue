<script setup>
// Nenhum código JavaScript no script setup, o que está correto se não houver lógica a ser adicionada.
</script>

<template>
  <div class="calculadora">
    <div>Teste</div>
    <div>Teste</div>
    <div>Teste</div>
    <div>Teste</div>
    <div>Teste</div>
    <div>Teste</div>
    <div>Teste</div>
    <div>Teste</div>
    <div>Teste</div>
    <div>Teste</div>
    <div>Teste</div>
    <div>Teste</div>
  </div>
</template>

<style scoped>
.calculadora {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
</style>
