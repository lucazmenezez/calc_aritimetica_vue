<script setup>
import { reactive } from 'vue';

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
  })

  // Calcula o resultado automaticamente quando qualquer valor dos campos ou a operação selecionada muda.
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
  <div class="container">
    <h1>Calculadora Aritimética</h1>
    <div class="campos">
      <!-- Liga os inputs diretamente ao estado e converte o valor para número automaticamente. -->
      <input v-model.number="estado.campo1" type="number" required placeholder="Insira um número">
      <input v-model.number="estado.campo2" type="number" required  placeholder="Insira um número">
      <!-- Liga a operação selecionada ao estado. -->
      <select v-model="estado.operacaoSelecionada">
        <option value="adicao">Adição +</option>
        <option value="subtracao">Subtração -</option>
        <option value="multiplicacao">Multiplicação *</option>
        <option value="divisao">Divisão /</option>
      </select>
      <div class="resultado">
        RESULTADO:
        <span>{{ resultado() }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
  * {
    font-family: sans-serif;
  }

  .container {
    max-width: 80%;
    margin: 0 auto;
    width: 100%;
    min-height: 100vh;
  }

  h1 {
    white-space: nowrap;
    text-align: center;
    color: green;
    font-size: 40px;
    letter-spacing: 1px;
  }

  @media (max-width: 767px) {

    h1 {
      white-space: wrap;
    }

  }

  .campos {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 40px 0;
    background-color: #ccc;
    border-radius: 8px;
  }

  .campos input,
  .campos select {
    margin-top: 12px;
    padding: 12px;
    font-size: 20px;
    font-weight: bold;
    outline: none;
    border-color: #000;
    border-radius: 12px;
    width: 300px;
  }

  .campos select {
    font-weight: 500;
    border-color: #000;
    width: calc(300px + 28px);
  }

  .resultado {
    padding: 12px;
    margin-top: 24px;
    font-size: 24px;
    font-weight: bold;
    letter-spacing: 1px;
    border: 4px dotted purple;
    color: purple;
  }

  .resultado span {
    margin-left: 12px;
  }
</style>
