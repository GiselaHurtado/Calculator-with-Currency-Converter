<script setup>
import { ref, onMounted } from 'vue';

// Asumimos que "today" es un objeto con una propiedad "p"
const weatherData = ref({
  title: '',
  today: {
    p: ''
  }
});
const skyImage = ref('');

onMounted(() => {
  fetchWeatherData();
});

const fetchWeatherData = async () => {
  try {
    const response = await fetch('https://www.el-tiempo.net/api/json/v2/provincias/33');
    const data = await response.json();
    weatherData.value.title = data.title;

    // Ahora usamos "p" como la propiedad que contiene el estado del cielo
    weatherData.value.today.p = data.today.p;
  
    // Actualizamos la llamada a getSkyImageUrl para pasar el estado del cielo correcto
    skyImage.value = await getSkyImageUrl(weatherData.value.today.p);
  } catch (error) {
    console.error('Error al obtener el tiempo:', error);
  }
};

const getSkyImageUrl = async (p) => {
  const pToImageUrl = {
    'despejado': '../assets/img/despejado.jpg',
    'nublado': '../assets/img/nublado.jpg',
    'lluvia': '../assets/img/lluvioso.jpg',
  };

  return Promise.resolve(pToImageUrl[p] || '../assets/img/desconocido.jpg');
};
</script>

<template>
  <div id="app">
    <div class="time-container">
      <h1>{{ weatherData.title }}</h1>
   
     
      <p>Estado del cielo: {{ weatherData.today.p }}</p>
    </div>
    <div class="sky-image">
      
      <img :src="skyImage" alt="Estado del cielo">
    </div>
  </div>
</template>
