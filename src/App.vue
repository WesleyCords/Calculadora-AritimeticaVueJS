<script setup>
  import { reactive, watch } from 'vue';

  const estado = reactive({
    operacao: '-',
    num1: 0,
    num2: 0,
    resultado: 0
  });

  const getNumeroOne = ev => estado.num1 = Number(ev.target.value);
  const getNumeroTwo = ev => estado.num2 = Number(ev.target.value);
  const mudaOperacao = ev => estado.operacao = ev.target.value;
  

  watch( () => [estado.operacao, estado.num1, estado.num2], () => {
    switch (estado.operacao) {
    case '+':
      estado.resultado = estado.num1 + estado.num2;
      break;
    case '-':
      estado.resultado = estado.num1 - estado.num2;
      break;
    case 'x':
      estado.resultado = estado.num1 * estado.num2;
      break;
    case '/':
      estado.resultado = estado.num2 !== 0 ? estado.num1 / estado.num2 : 'Erro: Divisão por zero';
      break;
    default: 
      estado.resultado = 0;
    }
  }, {immediate: true});

</script>

<template>
  <div class="container">
    <header>
      <h1>Calcularadora Aritimetica</h1>
    </header>
    <div class="grupo-input">
      <label for="num1">Primeiro Número</label>
      <input type="number" id="num1" placeholder="Digite aqui o número" @keyup="getNumeroOne">
    </div>
    <div class="set-operacao">
      <select @change="mudaOperacao" :value="estado.operacao">
        <option value="-">Subtração</option>
        <option value="+">Adição</option>
        <option value="x">Mutiplicação</option>
        <option value="/">Divisão</option>
      </select>
      <div class="view-operacao">
        Operação selecionada: {{ estado.operacao }}
      </div>
    </div>
    <div class="grupo-input">
      <label for="num1">Segundo Número</label>
      <input type="number" id="num2" placeholder="Digite aqui o número" @keyup="getNumeroTwo">
    </div>
    <h2>Resultado</h2>
    <span :class="{ 'erro': typeof estado.resultado === 'string' }"> {{ estado.resultado }}</span>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'poppins', sans-serif;
}
.container {
  background:  #1a2a6c;
  max-width: 450px;
  margin: 10px auto;
  padding: 15px 20px;
  border-radius: 20px;
  color: #f5f5f5;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.grupo-input,
.set-operacao {
  display: flex;
  flex-direction: column;
  gap: 5px;
}
.view-operacao {
  text-align: center;
  font-style: italic;
  font-size: 0.9rem;
}

input,
select {
  display: block;
  width: 100%;
  padding: 8px 20px;
  border: 2px solid #546cc9;
  outline: none;
  cursor: pointer;
  font-size: 1rem;
} 

h1,
h2,
span {
  text-align: center;
}

h1 {
  margin-bottom: 10px;
}
span {
  font-size: 2rem;
  font-weight: bold;
  margin-top: 10px;
}
.erro {
  color: #ff6b6b;
}
</style>
