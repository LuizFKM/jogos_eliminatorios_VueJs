<script setup>
import { defineProps } from 'vue';
const props = defineProps(['tabelaDosJogos','funcaoMontaTabela'])
</script>

<template>

    <div v-if="props.tabelaDosJogos" class="col-4 p-5 mt-5">
    <table class="table">
        <thead>
        <tr class="text-center">
            <th scope="col">Time 1</th>
            <th scope="col">X</th>
            <th scope="col">Time 2</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(jogo, index) in props.funcaoMontaTabela" :key="index">
            <td class="text-center">{{ jogo.time1 }}</td>
            <td class="text-center">X</td>
            <td class="text-center">{{ jogo.time2 }}</td>
        </tr>
        </tbody>
    </table>
    </div>

</template>