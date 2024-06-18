<script setup>
import { ref, computed } from 'vue';

// Definimos las propiedades reactivas
const amount = ref(0);
const currencyFrom = ref('EUR');
const currencyTo = ref('EUR');
const rates = {
  'EUR': 1,
  '$': 1.2,
  '¥': 0.0091,
  'HNL': 22.5
};

// Creamos una propiedad computada para el resultado
const result = computed(() => {
  return amount.value * rates[currencyFrom.value] / rates[currencyTo.value];
});

// Método para convertir la moneda
const convert = () => {
  amount.value = amount.value * rates[currencyFrom.value] / rates[currencyTo.value];
};
</script>

<template>
  <div>
    <input type="number" v-model.number="amount" placeholder="Cantidad" />
    <select v-model="currencyFrom">
      <option value="EUR">Euro (€)</option>
      <option value="$">Dólar ($)</option>
      <option value="¥">Yen (¥)</option>
      <option value="HNL">Lempira Hondureño (Honduras)</option>
    </select>
    <select v-model="currencyTo">
      <option value="EUR">Euro (€)</option>
      <option value="$">Dólar ($)</option>
      <option value="¥">Yen (¥)</option>
      <option value="HNL">Lempira Hondureño (Honduras)</option>
    </select>
    <button @click="convert()">Convertir</button>
    <p>{{ result }}</p>
  </div>
</template>
