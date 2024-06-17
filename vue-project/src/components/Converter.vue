<script setup>
new Vue({
    el: '#app',
    data: {
        amount: 0,
        currencyFrom: 'EUR',
        currencyTo: 'EUR',
        rates: {
            'EUR': 1,
            '$': 1.2,
            '¥': 0.0091,
            'HNL': 22.5
        }
    },
    computed: {
        result() {
            return this.amount * this.rates[this.currencyFrom] / this.rates[this.currencyTo];
        }
    },
    methods: {
        convert() {
            this.result = this.amount * this.rates[this.currencyFrom] / this.rates[this.currencyTo];
        }
    }
});

</script>

<template>
    
    <div id="app">
        <input type="number" v-model.number="amount" placeholder="Cantidad">
        <select v-model.number="currencyFrom">
            <option value="EUR">Euro (€)</option>
            <option value="$">Dólar ($)</option>
            <option value="¥">Yen (¥)</option>
            <option value="HNL">Lempira Hondureño (Honduras)</option>
        </select>
        <select v-model.number="currencyTo">
            <option value="EUR">Euro (€)</option>
            <option value="$">Dólar ($)</option>
            <option value="¥">Yen (¥)</option>
            <option value="HNL">Lempira Hondureño (Honduras)</option>
        </select>
        <button @click="convert">Convertir</button>
        <p>{{ result }}</p>
    </div>


</template>