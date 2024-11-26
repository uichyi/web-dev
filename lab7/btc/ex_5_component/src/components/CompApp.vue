<template>
  <div class="container mt-5">
    <div class="form-group">
      <label for="amount">Введите сумму:</label>
      <input type="number" v-model="amount" class="form-control" id="amount" placeholder="Сумма" />
    </div>
    <div class="form-group">
      <label for="currency">Выберите валюту:</label>
      <select v-model="country" class="form-control" id="currency">
        <option v-for="(rate, currency) in rates" :key="currency" :value="currency">
          {{ currency }}
        </option>
      </select>
    </div>
    <button @click="convert" class="btn btn-primary">Конвертировать</button>
    <div v-if="result" class="mt-3">
      <h5>{{ result }} BTC</h5>
    </div>
  </div>
</template>
  
<script>
export default {
  data() {
    return {
      amount: 0,
      country: 'USD',
      rates: {},
      result: null,
    };
  },
  created() {
    this.fetchRates();
  },
  methods: {
    async fetchRates() {
      const response = await fetch('https://api.coindesk.com/v1/bpi/currentprice.json');
      const data = await response.json();
      this.rates = data.bpi; 
    },
    convert() {
        const rate = this.rates[this.country].rate_float; 
        this.result = (this.amount / rate); 
    },
  },
};
</script>
