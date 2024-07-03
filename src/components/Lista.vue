<script setup>
import { defineProps } from 'vue';
const props = defineProps(['listaDosClubes', 'clubesCadastrados']);
</script>

<template>

    <div v-if="props.listaDosClubes" class="col-4 p-5 mt-5">
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="clube in props.clubesCadastrados" :key="clube">
        {{ clube }}
        </li>
    </ul>
    </div>

</template>
