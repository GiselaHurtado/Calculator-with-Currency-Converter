<script setup>
import { ref, onMounted } from 'vue';

const weatherData = ref({
  city: '',
  stateSky: ''
});
const skyImage = ref('');

onMounted(() => {
  fetchWeatherData();
});

const fetchWeatherData = async () => {
  try {
    const response = await fetch('https://www.el-tiempo.net/api/json/v2/provincias/33');
    const data = await response.json();
    weatherData.value.city = data.ciudades[0].name;
    weatherData.value.stateSky = data.ciudades[0].stateSky.description;

    skyImage.value = await getSkyImageUrl(weatherData.value.stateSky);
  } catch (error) {
    console.error('Error al obtener el tiempo:', error);
  }
};

const getSkyImageUrl = async (stateSky) => {
  const stateSkyToImageUrl = {
    despejado: '../assets/img/despejado.jpg',
    nublado: '../assets/img/nublado.jpg',
    lluvioso: '../assets/img/lluvioso.jpg',
    desconocido: '../assets/img/desconocido.jpg'
  };

  return Promise.resolve(stateSkyToImageUrl[stateSky] || '../assets/img/desconocido.jpg');
};

</script>

<template>
  <div id="app">
    <div class="time-container">
      <h1>{{ weatherData.city }}</h1>
      <p>Estado del cielo: {{ weatherData.stateSky }}</p>
    </div>
    <div class="sky-image">
      <img :src="skyImage" alt="Estado del cielo">
    </div>
  </div>
</template>
