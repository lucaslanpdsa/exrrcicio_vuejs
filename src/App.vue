<script setup>
import { reactive } from 'vue';

const estado = reactive({
  selected: " ",
  resultado: " ",
  operador: " ",
}
)
let calcula = (number1, number2) => {
  if (estado.selected == "Adição") {
    estado.resultado = Number(number1) + Number(number2)
    estado.operador = "+"
  }
  else if (estado.selected == "Subtração") {
    estado.resultado = Number(number1) - Number(number2)
    estado.operador = "-"
  }
  else if (estado.selected == "Multiplicação") {
    estado.resultado = Number(number1) * Number(number2)
    estado.operador = "*"
  }
  else if (estado.selected == "Divisão") {
    estado.resultado = Number(number1) / Number(number2)
    estado.operador = "/"
  } else {
    estado.resultado = "selecione uma operação"
  }
}
</script>

<template>
  <div
    class="container m-auto p-5 bg-light-subtle text-emphasis-light text-dark d-flex flex-column vh-100 justify-content-center">
    <header class="text-center mt-0 mb-2 m-auto
    p-2 ">
      <h1 class="fs-2">Calculadora</h1>
      <p class="fs-5">Selecione uma operação e preencha os dois campos</p>
    </header>
    <form @submit.prevent="(event) => { calcula(number1, number2), event.target.reset() }"
      class="d-flex justify-content-center gap-2 flex-wrap ">
      <select class="border border-black form-select w-25 text-center" @change="(e) => {
        estado.selected = e.target.value
        calcula(number1, number2)
      }">
        <option value="Adição">Adição</option>
        <option value="Subtração">Subtração</option>
        <option value="Multiplicação">Multiplicação</option>
        <option value="Divisão">Divisão</option>
      </select>
      <div class="w-100 justify-content-center d-flex gap-2 mb-3">
        <input type="number" @keyup="(e) => {
          number1 = e.target.value
          calcula(number1, number2)
        }" placeholder="numero" id="number1">
        <span class="fs-3">{{ estado.operador }}</span>
        <input @keyup="(e) => {
          number2 = e.target.value
          calcula(number1, number2)
        }" type="number" placeholder="numero" id="number2">
      </div>
    </form>
    <p class="w-100 text-center">{{ estado.resultado }}</p>
  </div>
</template>

<style scoped></style>
