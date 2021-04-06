<template>
  <div class="values" @change.prevent="onChange">
    <div class="from">
      <label>I have</label>
      <div class="select">
        <select 
          name="convertFrom"
          v-model="selectedFrom">
          <option 
            v-for="a in currencyFrom" 
            :key="a.ID">
            {{ a.CharCode }}
          </option>
        </select>
        <input 
          type="text" 
          name="from" 
          id=""
          v-model="convertFrom">
      </div>    
    </div>
    <div class="from">
      <label>I want to buy</label>
      <div class="select">
        <select 
          name="convertTo"
          v-model="selectedTo">
          <option  
            v-for="a in currencyFrom" 
            :key="a.ID">
            {{ a.CharCode }}
          </option>
        </select>
        <input 
          type="text" 
          name="to" 
          id=""
          v-model="convertTo">
      </div>    
    </div>
  </div>
</template>

<script>
  export default {
    props: {
        currencyFrom: {
          type: Object,
          required: false
        },
    },
    data() {
      return {
        convertFrom: null,
        convertTo: null,
        selectedFrom: '',
        selectedTo: ''
      }
    },
    methods: {
      onChange(e) {
        let name = e.target.name;
        if (this.selectedFrom && this.selectedTo) { 
          let initialFrom = this.currencyFrom[this.selectedFrom].Nominal * this.currencyFrom[this.selectedFrom].Value;
          let initialTo = this.currencyFrom[this.selectedTo].Nominal * this.currencyFrom[this.selectedTo].Value;
          if ( name === "from" || name === "convertFrom" ) {
            this.convertTo = (this.convertFrom * (initialFrom / initialTo)).toFixed(4);
          } else if ( name === "to" || name === "convertTo" ) {
            this.convertFrom = (this.convertTo * (initialTo / initialFrom)).toFixed(4);
          }
        }
      }
    }
  }
</script>


<style scoped>
.values {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.select {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.from {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: baseline;
}
select, label {
  width: 100px;
  font-size: 15px;

}
input, select {
  outline: 0;
  border-width: 0 0 2px;
  border-color: black
}
</style>
