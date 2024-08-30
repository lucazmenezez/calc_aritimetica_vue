<script setup>
  import { reactive } from 'vue';
  import Calculadora from './components/Calculadora.vue';

const estado = reactive({
  campo1: '',
  campo2: '',
  operacaoAritimetica: {
    adicao: (a, b) => a + b,
    subtracao: (a, b) => a - b,
    multiplicacao: (a, b) => a * b,
    divisao: (a, b) => a / b,
  },
  operacaoSelecionada: 'adicao',
});

function resultado() {
  const valor1 = parseFloat(estado.campo1);
  const valor2 = parseFloat(estado.campo2);

  if (isNaN(valor1) || isNaN(valor2)) {
    return 'Sem Valores';
  }

  const operacao = estado.operacaoAritimetica[estado.operacaoSelecionada];
  return operacao(valor1, valor2);
}

</script>

<template>
  <Calculadora 
    v-model:campo1="estado.campo1" 
    v-model:campo2="estado.campo2" 
    v-model:operacao="estado.operacaoSelecionada" 
    :resultado="resultado()"
  />
</template>