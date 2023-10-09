<script setup>
import { reactive } from 'vue';

const estado = reactive({
  numero1: 0,
  numero2: 0,
  conta: "somar",
  resultado: 0,
})

const executarConta = (e) => {

  if (e.target.id === 'num1') {
    estado.numero1 = parseInt(e.target.value)
  } else if (e.target.id === "num2") {
    estado.numero2 = parseInt(e.target.value)
  } else {
    estado.conta = e.target.value
  }

  const { conta } = estado

  switch (conta) {
    case "somar":
      return estado.resultado = estado.numero1 + estado.numero2
    case "subtrair":
      return estado.resultado = estado.numero1 - estado.numero2
    case "multiplicar":
      return estado.resultado = estado.numero1 * estado.numero2
    case "dividir":
      return estado.resultado = estado.numero1 / estado.numero2
  }
}
</script>

<template>
  <div class="container bg-dark text-white mt-2 rounded-2" style="height: 30rem;">
    <div class="d-flex w-50 flex-column container justify-content-center align-items-center">

      <h1 class="mb-5 mt-5">Calculadora com Vue JS</h1>

      <input @keyup="executarConta" placeholder="Número 1" id="num1" type="number"
        class="w-25 fs-5 p-2 mb-2 form-control">

      <select @change="executarConta" id="select" class="w-25 fs-5 p-2 mb-2 form-select">
        <option value="somar">Soma (+)</option>
        <option value="subtrair">Subtração (-)</option>
        <option value="multiplicar">Multiplicação (*)</option>
        <option value="dividir">divisão (/)</option>
      </select>

      <input @keyup="executarConta" placeholder="Número 2" id="num2" type="number"
        class="w-25 fs-5 p-2 mb-2 form-control">
      <p class="fs-2">=</p>
      <p class="fs-1 fw-bold">{{ estado.resultado }}</p>
    </div>
  </div>
</template>