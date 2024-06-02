<script setup>
import { ref } from 'vue';

const display = ref('0');
const currentInput = ref('');
const operator = ref(null);
const previousValue = ref(null);

const clear = () => {
  display.value = '0';
  currentInput.value = '';
  operator.value = null;
  previousValue.value = null;
};

const appendNumber = (number) => {
  if (currentInput.value.includes('.') && number === '.') return;
  currentInput.value = currentInput.value === '' ? number : currentInput.value + number;
  display.value = currentInput.value;
};

const chooseOperator = (op) => {
  if (currentInput.value === '') return;
  if (previousValue.value !== null) {
    compute();
  }
  operator.value = op;
  previousValue.value = currentInput.value;
  currentInput.value = '';
};

const compute = () => {
  let result;
  const prev = parseFloat(previousValue.value);
  const current = parseFloat(currentInput.value);
  if (isNaN(prev) || isNaN(current)) return;

  switch (operator.value) {
    case '+':
      result = prev + current;
      break;
    case '-':
      result = prev - current;
      break;
    case 'X':
      result = prev * current;
      break;
    case '÷':
      result = prev / current;
      break;
    default:
      return;
  }
  currentInput.value = result.toString();
  display.value = result.toString();
  operator.value = null;
  previousValue.value = null;
};

const handleEquals = () => {
  compute();
};

const handleDecimal = () => {
  if (!currentInput.value.includes('.')) {
    currentInput.value += '.';
  }
  display.value = currentInput.value;
};
</script>

<template>
  <div class="calculadora">
    <div class="display">{{ display }}</div>
    <div class="botao" @click="clear">C</div>
    <div class="botao">+/-</div>
    <div class="botao">%</div>
    <div class="botao operadores" @click="chooseOperator('÷')">÷</div>
    <div class="botao" @click="appendNumber('7')">7</div>
    <div class="botao" @click="appendNumber('8')">8</div>
    <div class="botao" @click="appendNumber('9')">9</div>
    <div class="botao operadores" @click="chooseOperator('X')">X</div>
    <div class="botao" @click="appendNumber('4')">4</div>
    <div class="botao" @click="appendNumber('5')">5</div>
    <div class="botao" @click="appendNumber('6')">6</div>
    <div class="botao operadores" @click="chooseOperator('-')">-</div>
    <div class="botao" @click="appendNumber('1')">1</div>
    <div class="botao" @click="appendNumber('2')">2</div>
    <div class="botao" @click="appendNumber('3')">3</div>
    <div class="botao operadores" @click="chooseOperator('+')">+</div>
    <div class="botao zero" @click="appendNumber('0')">0</div>
    <div class="botao" @click="handleDecimal">.</div>
    <div class="botao operadores" @click="handleEquals">=</div>
  </div>
</template>

<style scoped>

.calculadora {
  font-size: 40px;
  display: grid;
  width: 350px;
  text-align: center;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  padding: 0 10px;
}

.zero {
  grid-column: 1 / 3;
}

.botao {
  background-color: #f2f2f2;
  border: 1px solid #999;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}

.operadores {
  background-color: orange;
  color: white;
}
</style>
