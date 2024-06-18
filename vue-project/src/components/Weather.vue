<script setup>
import { ref, onMounted } from 'vue';

const today = ref('');
const skyImage = ref('');

onMounted(() => {
  fetchTime();
  fetchSkyImage();
});

const fetchTime = async () => {
  try {
    const response = await fetch('https://www.el-tiempo.net/api/json/v2/provincias/33');
    const data = await response.json();
    today.value = data.today;
  } catch (error) {
    console.error('Error al obtener el tiempo:', error);
  }
};

const fetchSkyImage = async () => {
  // Suponiendo que tienes una función que devuelve la URL de la imagen basada en el estado del tiempo
  skyImage.value = await getSkyImageUrl('estado_del_cielo');
};

// Esta es una función de ejemplo que necesitarías definir
// para obtener la URL de la imagen basada en el estado del tiempo
const getSkyImageUrl = (weatherState) => {
  // Aquí iría la lógica para obtener la URL de la imagen
  // Por ejemplo, podrías usar una API como OpenWeatherMap
  // y luego devolver la URL de la imagen correspondiente al estado del tiempo
  return 'url_de_la_imagen_del_estado_del_cielo';
};
</script>

<template>
  <div id="app">
    <div class="time-container">
      <h1>El Tiempo en Asturias</h1>
      <p>{{ today }}</p>
    </div>
    <div class="sky-image">
      <img :src="skyImage" alt="Estado del cielo">
    </div>
  </div>
</template>
