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
  
  <script>
  export default {
    data() {
      return {
        display: '0',
        buttons: [
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
        ]
      };
    },
    methods: {
      handleClick(button) {
        switch (button.type) {
          case 'number':
            this.appendNumber(button.text);
            break;
          case 'operator':
            this.appendOperator(button.text);
            break;
          case 'equals':
            this.calculate();
            break;
          case 'delete':
            this.deleteLast();
            break;
          case 'clear':
            this.clearDisplay();
            break;
        }
      },
      clearDisplay() {
        this.display = '0';
      },
      deleteLast() {
        if (this.display.length > 1) {
          this.display = this.display.slice(0, -1);
        } else {
          this.display = '0';
        }
      },
      appendNumber(number) {
        if (this.display === '0') {
          this.display = number;
        } else {
          this.display += number;
        }
      },
      appendOperator(operator) {
        const lastChar = this.display.slice(-1);
        if (['+', '-', '*', '/'].includes(lastChar)) {
          this.display = this.display.slice(0, -1) + operator;
        } else {
          this.display += operator;
        }
      },
      calculate() {
        try {
          this.display = eval(this.display);
        } catch {
          this.display = 'Error';
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .calculator {
    border: 1px solid #ccc;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    overflow: hidden;
    width: 320px;
    background-color: white;
    margin: 50px auto;
  }
  .display {
    background-color: #222;
    color: white;
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
    background-color: #eee;
    border: 1px solid #ccc;
    font-size: 1.5em;
    padding: 20px;
    cursor: pointer;
    transition: background-color 0.2s;
    box-sizing: border-box;
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
  