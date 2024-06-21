<script setup>
import { ref } from 'vue';

const display = ref('0');

const buttons = [
  { text: '7', class: 'btn', type: 'number' },
  { text: '8', class: 'btn', type: 'number' },
  { text: '9', class: 'btn', type: 'number' },
  { text: '+', class: 'btn', type: 'operator' },
  { text: '4', class: 'btn', type: 'number' },
  { text: '5', class: 'btn', type: 'number' },
  { text: '6', class: 'btn', type: 'number' },
  { text: '-', class: 'btn', type: 'operator' },
  { text: '1', class: 'btn', type: 'number' },
  { text: '2', class: 'btn', type: 'number' },
  { text: '3', class: 'btn', type: 'number' },
  { text: '*', class: 'btn', type: 'operator' },
  { text: '.', class: 'btn', type: 'number' },
  { text: '0', class: 'btn', type: 'number' },
  { text: '=', class: 'btn', type: 'equals' },
  { text: '/', class: 'btn', type: 'operator' },
  { text: '←', class: 'btn', type: 'delete' },
  { text: 'C', class: 'btn', type: 'clear' }
];

function handleClick(button) {
  switch (button.type) {
    case 'number':
      appendNumber(button.text);
      break;
    case 'operator':
      appendOperator(button.text);
      break;
    case 'equals':
      calculate();
      break;
    case 'delete':
      deleteLast();
      break;
    case 'clear':
      clearDisplay();
      break;
  }
}

function clearDisplay() {
  display.value = '0';
}

function deleteLast() {
  if (display.value.length > 1) {
    display.value = display.value.slice(0, -1);
  } else {
    display.value = '0';
  }
}

function appendNumber(number) {
  if (display.value === '0') {
    display.value = number;
  } else {
    display.value += number;
  }
}

function appendOperator(operator) {
  const lastChar = display.value.slice(-1);
  if (['+', '-', '*', '/'].includes(lastChar)) {
    display.value = display.value.slice(0, -1) + operator;
  } else {
    display.value += operator;
  }
}

function calculate() {
  try {
    display.value = eval(display.value);
  } catch {
    display.value = 'Error';
  }
}
</script>

<template>
  <div class="calculator">
    <div class="display">{{ display }}</div>
    <div class="buttons">
      <button v-for="button in buttons" :key="button.text" :class="button.class" @click="handleClick(button)">
        {{ button.text }}
      </button>
    </div>
  </div>
</template>

<style scoped>
.calculator {
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  width: 320px;
  background-color: rgb(100,180,250);
  margin: 50px auto;
}
.display {
  background-color: #222;
  color: rgb(120,175,225);
  font-size: 2em;
  padding: 20px;
  text-align: right;
  box-sizing: border-box;
}
.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
}
.btn {
  background-color: rgb(50,75,150);
  color: white;
  border: 1px solid #ccc;
  font-size: 1.5em;
  padding: 20px;
  cursor: pointer;
  transition: background-color 0.2s;
  box-sizing: border-box;
  border-radius: 100px;
}
.btn:hover {
  background-color: #ddd;
}
.btn:active {
  background-color: #ccc;
}
.span-two {
  grid-column: span 2;
}
</style>
