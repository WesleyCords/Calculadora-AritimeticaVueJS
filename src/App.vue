<script setup>
  import { reactive } from 'vue';

  let estado = reactive({
    operacao: '-',
    numero1: 21,
    numero2: 2,
    resultado: 0
  });

  const mudaOperacao = ev => estado.operacao = ev.target.value;

  if (estado.operacao === '-') {
    estado.resultado = estado.numero1 - estado.numero2;
  }

  const getNumeroOne = ev => estado.numero1 = Number(ev.target.value);
  const getNumeroTwo = ev => estado.numero2 = Number(ev.target.value);


  switch (estado.operacao) {
    case '+':
      estado.resultado = estado.numero1 + estado.numero2;
      break;
    case '-':
      estado.resultado = estado.numero1 - estado.numero2;
      break;
    case 'x':
      estado.resultado = estado.numero1 * estado.numero2;
      break;
    case '/':
      estado.resultado = estado.numero2 !== 0 ? estado.numero1 / estado.numero2 : 'Erro: Divisão por zero';
      break;
  };

</script>

<template>
  <div class="container">
    <h1>Calcularadora Aritimetica</h1>
    <div class="input-num1">
      <label for="num1">Primeiro Número</label>
      {{ estado.numero1 }}
      <input type="number" id="num1" placeholder="Digite aqui o número" @keyup="getNumeroOne">
    </div>
    <select @change="mudaOperacao">
      <option value="-">Subtração</option>
      <option value="+">Sumando</option>
      <option value="x">Mutiplicação</option>
      <option value="/">Divisão</option>
    </select>
    {{ estado.operacao }}
      <div class="input-num2">
      <label for="num1">Segundo Número</label>
      <input type="number" id="num2" placeholder="Digite aqui o número" @keyup="getNumeroTwo">
      {{ estado.numero2 }}
    </div>
    <h2>Resultado</h2>
    <span>{{ estado.resultado }}</span>
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
  min-height: 70vh;
  margin: 50px auto;
  padding: 30px 40px;
  border-radius: 20px;
  color: #f5f5f5;
  display: flex;
  flex-direction: column;
  gap: 20px;
}
input,
select {
  display: block;
  width: 100%;
  padding: 5px 20px;
  border: 2px solid #546cc9;
  outline: none;
  cursor: pointer;
}
h1,
h2,
span {
  text-align: center;
}
span {
  font-size: 2rem;
  font-weight: bold;
}
.erro {
  color: red;
}
</style>
