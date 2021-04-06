<template>
<div>
  <h1>Currency Converter</h1>  
  <ExchangeField 
    :currencyFrom="currencyFrom"
  />
  </div>
</template>

<script>
import ExchangeField from './components/ExchangeField.vue'

export default {
  name: 'App',
  components: {
    ExchangeField
  },
  data() {
    return {
      currencyFrom: null      
    }
  },
  created() {
    fetch("https://www.cbr-xml-daily.ru/daily_json.js")
      .then( async response => {
        const data = await response.json();

        if (!response.ok) {
          const error = (data && data.message) || response.statusText;
          return Promise.reject(error);
        }

        this.currencyFrom = data.Valute
      })
      .catch(error => {
        this.errorMessage = error;
        console.error("There was an error!", error);
      });
  }
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
