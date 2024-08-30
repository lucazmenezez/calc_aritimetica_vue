<script setup>
    const props = defineProps(['campo1', 'campo2', 'operacao', 'resultado'])
    const emit = defineEmits(['update:campo1', 'update:campo2', 'update:operacao']);

    function updateCampo1(event) {
        emit('update:campo1', event.target.value);
    }

    function updateCampo2(event) {
        emit('update:campo2', event.target.value);
    }

    function updateOperacao(event) {
        emit('update:operacao', event.target.value);
    }
</script>

<template>
    <div class="container">
        <h1>Calculadora Aritimética</h1>
        <div class="campos">
            <input v-model.number="props.campo1" @input="updateCampo1" type="number" required placeholder="Insira um número">
            <input v-model.number="props.campo2" @input="updateCampo2" type="number" required placeholder="Insira um número">
            <select v-model="props.operacao" @change="updateOperacao">
                <option value="adicao">Adição +</option>
                <option value="subtracao">Subtração -</option>
                <option value="multiplicacao">Multiplicação *</option>
                <option value="divisao">Divisão /</option>
            </select>
            <div class="resultado">
                RESULTADO:
                <span>{{ props.resultado }}</span>
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