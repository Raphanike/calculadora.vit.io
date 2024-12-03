<script setup>
import { ref, computed } from 'vue'

const num1 = ref(null)
const num2 = ref(null)
const resultado = ref(null)
const erro = ref(false)

const mensagem = computed(() => {
  return erro.value ? resultado.value : `O resultado é: ${resultado.value}`
})

const calcular = (operacao) => {
  const n1 = parseFloat(num1.value)
  const n2 = parseFloat(num2.value)

  if (isNaN(n1) || isNaN(n2)) {
    resultado.value = 'Por favor, insira números válidos.'
    erro.value = true
    return
  }

  erro.value = false
  let res

  switch (operacao) {
    case '+':
      res = n1 + n2
      break
    case '-':
      res = n1 - n2
      break
    case '*':
      res = n1 * n2
      break
    case '/':
      if (n2 === 0) {
        res = 'Erro: Divisão por zero!'
        erro.value = true
      } else {
        res = n1 / n2
      }
      break
    default:
      res = 'Operação inválida.'
      erro.value = true
  }

  resultado.value = res
}

const resetar = () => {
  num1.value = null
  num2.value = null
  resultado.value = null
  erro.value = false
}
</script>

<template>
  <div class="calculator">
    <h1>Calculadora</h1>
    <input
      v-model.number="num1"
      type="number"
      placeholder="Número 1"
      class="input"
    />
    <input
      v-model.number="num2"
      type="number"
      placeholder="Número 2"
      class="input"
    />
    <div class="buttons">
      <button @click="calcular('+')">+</button>
      <button @click="calcular('-')">-</button>
      <button @click="calcular('*')">×</button>
      <button @click="calcular('/')">÷</button>
    </div>
    <div v-if="resultado !== null" class="result">
      <h2>{{ mensagem }}</h2>
    </div>
    <button class="reset" @click="resetar">Redefinir</button>
  </div>
</template>

<style scoped>
.calculator {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  font-size: 24px;
  margin-bottom: 20px;
}

.input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.buttons {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}

button {
  padding: 10px 15px;
  font-size: 16px;
  border: none;
  background-color: #007bff;
  color: white;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

.reset {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  background-color: #dc3545;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.reset:hover {
  background-color: #a71d2a;
}

.result {
  text-align: center;
  margin-top: 20px;
  font-size: 18px;
}

.result h2 {
  color: #333;
}

.error {
  color: red;
}
</style>
