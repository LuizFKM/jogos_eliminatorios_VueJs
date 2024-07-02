<script setup>
import { reactive } from 'vue';

const estado = reactive({
  cadastraTime: '',
  timesCadastrados: [],
  listaDeClubes: false,
  tabelaDeJogos: false,
});

const cadastrarClube = () => {
  const clube = estado.cadastraTime;
  if (clube.length > 3) {
    alert('Clube cadastrado com sucesso!');
    estado.timesCadastrados.push(clube);
    estado.cadastraTime = '';
  } else {
    alert('Nome do clube inválido');
  }
};

const listaClubes = () => {
  estado.listaDeClubes = true;
};

const montaTabelaDeJogos = () => {
  const tam = estado.timesCadastrados.length;
  if (tam === 0 || tam % 2 === 1) {
    alert("Deve haver número par de clubes");
    return [];
  }

  let jogos = [];
  const ultimo = estado.timesCadastrados.length - 1;

  for (let i = 0; i < tam / 2; i++) {
    const jogo = {
      time1: estado.timesCadastrados[i],
      time2: estado.timesCadastrados[ultimo - i]
    };
    jogos.push(jogo);
  }
  estado.tabelaDeJogos = true;
  return jogos;
};
</script>

<template>
  <header class="p-5 mt-5 text-center border-2 border-bottom border-success">
    <h1>Jogos Eliminatórios</h1>
  </header>
  <div class="row">
    <div class="col-6 p-5 mt-5">
      <form @submit.prevent="">
        <div class="input-group mb-3">
          <input 
            type="text" 
            class="form-control" 
            placeholder="Digite o nome do clube" 
            v-model="estado.cadastraTime"
          >
          <button type="button" class="btn btn-secondary" @click="cadastrarClube">Cadastrar</button>
        </div>
        <button type="button" id="btn-lista" class="me-2 btn btn-outline-secondary" @click="listaClubes">Listar clubes</button>
        <button type="button" class="btn btn-outline-secondary" @click="montaTabelaDeJogos">Montar tabela de jogos</button>
      </form>
    </div>
    <div v-if="estado.listaDeClubes" class="col-6 p-5 mt-5">
      <ul class="list-group mt-4">
        <li class="list-group-item" v-for="clube in estado.timesCadastrados" :key="clube">
          {{ clube }}
        </li>
      </ul>
    </div>
    <div v-if="estado.tabelaDeJogos" class="col-6 p-5 mt-5">
      <table class="table">
        <thead>
          <tr class="text-center">
            <th scope="col">Time 1</th>
            <th scope="col">X</th>
            <th scope="col">Time 2</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(jogo, index) in montaTabelaDeJogos()" :key="index">
            <td class="text-center">{{ jogo.time1 }}</td>
            <td class="text-center">X</td>
            <td class="text-center">{{ jogo.time2 }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
</style>
