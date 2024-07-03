<script setup>
import { defineProps } from 'vue';

const props = defineProps(['cadastrarTime', 'cadastrarClube', 'listarClubes', 'montarTabelaDeJogos']);
</script>

<template>
  <div class="col-4 p-5 mt-5 align-middle" >
    <form @submit.prevent="">
      <div class="input-group mb-3">
        <input 
          type="text" 
          class="form-control" 
          placeholder="Digite o nome do clube" 
          @change="props.cadastrarTime"
        >
        <button type="button" class="btn btn-secondary" @click="cadastrarClube">Cadastrar</button>
      </div>
      <button type="button" id="btn-lista" class="me-2 btn btn-outline-secondary" @click="listarClubes">Listar clubes</button>
      <button type="button" class="btn btn-outline-secondary" @click="montarTabelaDeJogos">Montar tabela de jogos</button>
    </form>
  </div>
</template>
