<template>
    <div class="col-md-9 p-5" v-if="showCurrencyConverterComponent">
        <div class="text-center mb-5">
            <h1>Currency Converter</h1>
        </div>
        <div class="form-group">
            <label style="font-weight: bold;">Input amount:</label>
            <input type="number" id="amount" max="30" v-model="amount" class="form-control mt-2" placeholder="Input amount here" >
        </div>
        <div class="container">
            <div class="row mt-3">
                <div class="col-md-6">
                    <div class="form-group">
                        <label style="font-weight: bold;">From:</label>
                        <select class="form-select" id="fromCurrency" v-model="fromCurrency">
                            <option v-for="currency in currencies" :key="currency">{{ currency }}</option>
                        </select>
                    </div>
                    
                </div>
                <div class="col-md-6">
                    <div class="form-group">
                        <label style="font-weight: bold;">To:</label>
                        <select class="form-select" id="toCurrency" v-model="toCurrency">
                            <option v-for="currency in currencies" :key="currency">{{ currency }}</option>
                        </select>
                    </div>
                </div>
                <div class="mt-5 d-flex justify-content-center">
                    <button class="btn btn-warning mx-1" @click="convert">Convert</button>
                    <button v-if="result !== null" class="btn btn-success mx-1" @click="clear">Clear</button>
                </div>
            </div>
        </div>

        

        <div v-if="result !== null" class="mt-3">
            <h5>Result:</h5>
            <textarea style="font-weight: bold; font-size: 30px" class="form-control text-center p-5" rows="1" readonly>{{ amount }} {{ fromCurrency }} is equivalent to {{ result }}</textarea>
            
        </div>
             
    </div>
</template>

<script>
export default {
    props: ['showCurrencyConverterComponent'],
  data() {
    return {
      amount: 1,
      fromCurrency: 'USD',
      toCurrency: 'EUR',
      currencies: ['USD', 'EUR', 'GBP', 'JPY', 'CAD'], // Add more currencies as needed
      result: null,
    };
  },
  methods: {
    async convert() {
      try {
        const response = await fetch(`https://api.exchangerate-api.com/v4/latest/${this.fromCurrency}`);
        const data = await response.json();

        if (data.rates && data.rates[this.toCurrency]) {
          const rate = data.rates[this.toCurrency];
          this.result = (this.amount * rate).toFixed(2);
        } else {
          console.error('Invalid currency codes');
        }
      } catch (error) {
        console.error('Error fetching exchange rates:', error);
      }
    },
    clear(){
        this.result = null;
    }
  },
};
</script>