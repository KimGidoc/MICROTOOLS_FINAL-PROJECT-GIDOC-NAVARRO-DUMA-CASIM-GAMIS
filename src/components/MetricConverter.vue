<template>
    <div class="col-md-9 p-5" v-if="showMetricConverterComponent">
        <div class="text-center mb-5">
            <h1>Currency Converter</h1>
        </div>
        <div class="form-group">
            <label style="font-weight: bold;">Input Value:</label>
            <input type="number" id="value" max="30" v-model="value" class="form-control mt-2" placeholder="Input amount here"  :disabled="result">
        </div>
        <div class="container">
            <div class="row mt-3">
                <div class="col-md-6">
                    <div class="form-group">
                        <label style="font-weight: bold;">From:</label>
                        <select class="form-select" id="fromUnit" v-model="fromUnit" :disabled="result">
                            <option v-for="unit in metricUnits" :key="unit">{{ unit }}</option>
                        </select>
                    </div>
                    
                </div>
                <div class="col-md-6">
                    <div class="form-group">
                        <label style="font-weight: bold;">To:</label>
                        <select class="form-select" id="toUnit" v-model="toUnit" :disabled="result">
                            <option v-for="unit in metricUnits" :key="unit">{{ unit }}</option>
                        </select>
                    </div>
                </div>
                <div class="mt-5 d-flex justify-content-center">
                    <button class="btn btn-primary mx-1" @click="convert" v-if="result == null">Convert</button>
                    <button v-if="result !== null" class="btn btn-warning mx-1" @click="clear">Try Again</button>
                </div>
            </div>
        </div>

        <div v-if="result !== null" class="mt-3">
            <h5>Result:</h5>
            <textarea style="font-weight: bold; font-size: 30px" class="form-control text-center p-5" rows="1" readonly>{{ value }} {{ fromUnit }} is equivalent to {{ result }} {{ toUnit }}</textarea>
            
        </div>
             
    </div>
</template>

<script>
export default {
    props: ['showMetricConverterComponent'],
    data() {
    return {
      value: 1,
      fromUnit: 'Kilometer',
      toUnit: 'Meter',
      metricUnits: ['Kilometer', 'Hectometer', 'Decameter', 'Meter', 'Decimeter', 'Centimeter', 'Millimeter'],
      conversionFactors: {
        'Kilometer': {
          'Hectometer': 10,
          'Decameter': 100,
          'Meter': 1000,
          'Decimeter': 10000,
          'Centimeter': 100000,
          'Millimeter': 1000000,
        },
        'Hectometer': {
          'Kilometer': 0.1,
          'Decameter': 10,
          'Meter': 100,
          'Decimeter': 1000,
          'Centimeter': 10000,
          'Millimeter': 100000,
        },
        'Decameter': {
          'Kilometer': 0.01,
          'Hectometer': 0.1,
          'Meter': 10,
          'Decimeter': 100,
          'Centimeter': 1000,
          'Millimeter': 10000,
        },
        'Meter': {
          'Kilometer': 0.001,
          'Hectometer': 0.01,
          'Decameter': 0.1,
          'Decimeter': 10,
          'Centimeter': 100,
          'Millimeter': 1000,
        },
        'Decimeter': {
          'Kilometer': 0.0001,
          'Hectometer': 0.001,
          'Decameter': 0.01,
          'Meter': 0.1,
          'Centimeter': 10,
          'Millimeter': 100,
        },
        'Centimeter': {
          'Kilometer': 0.00001,
          'Hectometer': 0.0001,
          'Decameter': 0.001,
          'Meter': 0.01,
          'Decimeter': 0.1,
          'Millimeter': 10,
        },
        'Millimeter': {
          'Kilometer': 0.000001,
          'Hectometer': 0.00001,
          'Decameter': 0.0001,
          'Meter': 0.001,
          'Decimeter': 0.01,
          'Centimeter': 0.1,
        },
      },
      result: null,
    };
  },
  methods: {
    convert() {
      const conversionFactor = this.conversionFactors[this.fromUnit][this.toUnit];

      if (conversionFactor !== undefined) {
        this.result = (this.value * conversionFactor);
      } else {
        console.error('Invalid conversion units');
      }
    },
    clear(){
        this.result = null;
    }
  },
};
</script>
