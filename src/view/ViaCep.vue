<template>
  <div>
    <h1>Consultar CEP</h1>
    <hr>
    <form action="#" @submit.prevent="getCep">
      <label for="cep"><h2>Digite o CEP: </h2></label>
      <input type="text" id="cep" v-model="cep">
      
      <label for="format"><h2>Escolha o formato: </h2></label>
      <select v-model="selectedFormat" id="format">
        <option value="json">JSON</option>
      </select>

      <input type="submit" value="Consultar">
      
      <div>
        <p><h3>Rua: {{ place.street }} </h3></p>
        <p><h3>Bairro: {{ place.neighborhood }}</h3></p>
        <p><h3>Cidade: {{ place.city }} / {{ place.state }}</h3></p>
      </div>
    </form>
  </div>
</template>

<script setup>
import axios from 'axios'
import { ref } from 'vue'
import { reactive } from 'vue'

const baseUrl = 'https://viacep.com.br/ws/'
const cep = ref("");
const place = reactive({
  street: '',
  neighborhood: '',
  city: '',
  state: ''
});
const selectedFormat = ref("");

const getCep = () => {
  const format = `/${selectedFormat.value}`;
  axios.get(baseUrl + cep.value + format)
    .then((response) => {
        console.log(response);
      // Trata os diferentes formatos de resposta
      if (selectedFormat.value === 'json') {
        place.street = response.data.logradouro;
        place.neighborhood = response.data.bairro;
        place.city = response.data.localidade;
        place.state = response.data.uf;
      }
    })
    .catch((error) => {
      console.error('Eita.. deu erro!', error)
    });
}
</script>

<style scoped>
/* Adicione estilos conforme necessário */
</style>
