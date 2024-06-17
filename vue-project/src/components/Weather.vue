<script setup>

new Vue({
    el: '#app',
    data: {
        today: '',
        skyImage: ''
    },
    mounted() {
        this.fetchTime();
        this.fetchSkyImage();
    },
    methods: {
        fetchTime() {
            fetch('https://www.el-tiempo.net/api/json/v2/provincias/33')
                .then(response => response.json())
                .then(data => {
                    // Aquí procesas los datos y actualizas el estado de 'tiempo'
                    this.today = data.today;
                })
                .catch(error => {
                    console.error('Error al obtener el tiempo:', error);
                });

        },
        fetchSkyImage() {
            // Aquí iría la lógica para obtener el estado del cielo de la API de El Tiempo
            // y luego actualizar el estado de 'skyImage' con la URL de la imagen correspondiente.
            // Este es solo un ejemplo y no funcionará sin la URL real de la API y los datos correctos.
            this.skyImage = 'url_de_la_imagen_del_estado_del_cielo';
        }
    }
});

</script>


<template>

    <body>
        <main>
            <Weather />

        </main>
        <div id="app">
            <div class="time-container">
                <h1>El Tiempo en Asturias</h1>
                <p>{{ today }}</p>
            </div>
            <div class="sky-image">
                <img :src="skyImage" alt="Estado del cielo">
            </div>
        </div>
    </body>
</template>

<style>
/* @media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
} */
</style>