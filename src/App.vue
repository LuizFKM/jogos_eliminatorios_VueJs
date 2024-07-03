<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import Lista from './components/Lista.vue';
import Tabela from './components/Tabela.vue';

const estado = reactive({
  cadastraTime: '',
  timesCadastrados: [],
  listaDeClubes: false,
  tabelaDeJogos: false,
  jogos: []
});

const cadastrarClube = () => {
  const clube = estado.cadastraTime;
  console.log("Cadastrando clube: ", clube)
  if (clube.length >= 3) {
    alert('Clube cadastrado com sucesso!');
    estado.timesCadastrados.push(clube);
    estado.cadastraTime = '';
  } else {
    alert('Nome do clube inválido');
  }
};

const cadastra = (evento) => {
  return estado.cadastraTime = evento.target.value
}

const listaClubes = () => {
  console.log('Listando clubes');
  estado.listaDeClubes = true;
};

const montaTabelaDeJogos = () => {
  console.log('Montando tabela de jogos');
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
  estado.jogos = jogos;
  estado.tabelaDeJogos = true;
};




console.log(estado)


</script>

<template>
  <Cabecalho />
  <div class="row text-center ">

  <Formulario 
    :cadastrar-time="cadastra" 
    :cadastrar-clube="cadastrarClube" 
    :listar-clubes="listaClubes" 
    :montar-tabela-de-jogos="montaTabelaDeJogos"
  />
  <Lista :lista-dos-clubes="estado.listaDeClubes" :clubes-cadastrados="estado.timesCadastrados" />
  <Tabela :tabela-dos-jogos="estado.tabelaDeJogos" :funcao-monta-tabela="estado.jogos" />
  </div>
</template>
