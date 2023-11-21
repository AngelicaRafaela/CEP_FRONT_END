<template>
  
  <div class="app-container">

    <ul>
      <li><router-link to="/"><h1>Início</h1></router-link></li>
      <li><router-link to="Via-Cep"><h1>Via Cep</h1></router-link></li>
      <li><router-link to="About"><h1>Sobre</h1></router-link></li>
    </ul>

    <router-view />

  </div>


</template>

<script setup>

</script>

<style scoped>
@import 'tailwindcss/base';
@import 'tailwindcss/components';
@import 'tailwindcss/utilities';

</style>