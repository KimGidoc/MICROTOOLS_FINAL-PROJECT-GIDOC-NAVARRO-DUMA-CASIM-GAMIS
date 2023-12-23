
<template>
  <header>
      <div class="d-flex justify-content-center align-items-center bg-success text-white" style="border-bottom: 3px solid #adadad;">
        <div class="p-4">
          <h1 class="text-primary" style="font-size: 90px;">Microtool Project</h1>
          <h5 class="text-warning text-center">A project for Advance Web Application <span class="text-light">||</span> Vue.js and Bootstrap 5</h5>
        </div>
      </div>
  </header>
  <div class="container py-3" style="height: 100vh;">
    <div class="row">
      <div class="col-md-3" style="border-right: 3px solid #adadad;">
        
          <h3>Tools</h3>
          
          <div class="card mt-3" :class="flexBox">
              <a @click="showFlexbox" class="text-decoration-none" >
                <div class="card-body">
                  <h5 class="card-title">Flexbox</h5>
                  <p class="card-text">A CSS layout module.</p>
                </div>
              </a>
          </div>
          <div class="card mt-3" :class="CurrencyCon">
              <a @click="showCurrencyConverter" class="text-decoration-none" >
                <div class="card-body">
                  <h5 class="card-title">Currency Converter</h5>
                  <p class="card-text">A tool for curency conversions.</p>
                </div>
              </a>
          </div>
          <div @click="showPasswordGenerator" class="card mt-3" :class="passGen">
              <a href="javascript: void(0)" class="text-decoration-none">
                <div class="card-body">
                  <h5 class="card-title">Password Generator</h5>
                  <p class="card-text">A tool for generating random password.</p>
                </div>
              </a>
          </div>
          <div @click="showCountdownTimer" class="card mt-3" :class="countTimer">
              <a href="javascript: void(0)" class="text-decoration-none">
                <div class="card-body">
                  <h5 class="card-title">Countdown Timer</h5>
                  <p class="card-text">A countdown timer toool.</p>
                </div>
              </a>
          </div>
          <div @click="showMetricConverter" class="card mt-3" :class="metricCon">
              <a href="javascript: void(0)" class="text-decoration-none">
                <div class="card-body">
                  <h5 class="card-title">Metric Converter</h5>
                  <p class="card-text">A tool for metric conversions.</p>
                </div>
              </a>
          </div>
      </div>
      <Flexbox :showFlexboxComponent="showFlexboxComponent"/>
      <CurrencyConverter :showCurrencyConverterComponent = "showCurrencyConverterComponent"/>
      <PasswordGenerator :showPasswordGeneratorComponent="showPasswordGeneratorComponent"/> 
      <CountdownTimer :showCountdownTimerComponent="showCountdownTimerComponent"/>
      <MetricConverter :showMetricConverterComponent="showMetricConverterComponent"/>
    </div>
  </div>
</template>

<script>
  import Flexbox from './components/Flexbox.vue'
  import CurrencyConverter from './components/CurrencyConverter.vue'
  import PasswordGenerator from './components/PasswordGenerator.vue'
  import CountdownTimer from './components/CountdownTimer.vue'
  import MetricConverter from './components/MetricConverter.vue'

  export default{
    components: {Flexbox, CurrencyConverter, CountdownTimer, MetricConverter, PasswordGenerator},
    data(){
      return{
        showMetricConverterComponent: false,
        showFlexboxComponent: true,
        showCurrencyConverterComponent: false,
        showPasswordGeneratorComponent: false,
        showCountdownTimerComponent: false,
        flexBox: 'active',
        CurrencyCon: '',
        passGen: '',
        countTimer: '',
        metricCon: '',
      }
    },
    methods: {
      showFlexbox(){
        this.showFlexboxComponent = true
        this.showPasswordGeneratorComponent = false
        this.showCurrencyConverterComponent = false
        this.showCountdownTimerComponent = false
        this.showMetricConverterComponent = false
        this.flexBox = 'active'
        this.CurrencyCon = ''
        this.passGen = ''
        this.countTimer = ''
        this.metricCon = ''

      },
      showCurrencyConverter(){
        this.showFlexboxComponent = false
        this.showCurrencyConverterComponent = true
        this.showPasswordGeneratorComponent = false
        this.showCountdownTimerComponent = false
        this.showMetricConverterComponent = false
        this.flexBox = ''
        this.CurrencyCon = 'active'
        this.passGen = ''
        this.countTimer = ''
        this.metricCon = ''
      },
      showPasswordGenerator(){
        this.showFlexboxComponent = false
        this.showCurrencyConverterComponent = false
        this.showPasswordGeneratorComponent = true
        this.showCountdownTimerComponent = false
        this.showMetricConverterComponent = false
        this.flexBox = ''
        this.CurrencyCon = ''
        this.passGen = 'active'
        this.countTimer = ''
        this.metricCon = ''
      },
      showCountdownTimer(){
        this.showFlexboxComponent = false
        this.showCurrencyConverterComponent = false
        this.showPasswordGeneratorComponent = false
        this.showCountdownTimerComponent = true
        this.showMetricConverterComponent = false
        this.flexBox = ''
        this.CurrencyCon = ''
        this.passGen = ''
        this.countTimer = 'active'
        this.metricCon = ''
      },
      showMetricConverter(){
        this.showFlexboxComponent = false
        this.showCurrencyConverterComponent = false
        this.showPasswordGeneratorComponent = false
        this.showCountdownTimerComponent = false
        this.showMetricConverterComponent = true
        this.flexBox = ''
        this.CurrencyCon = ''
        this.passGen = ''
        this.countTimer = ''
        this.metricCon = 'active'
      }
    }
  }
</script>

<style>
  div .active{
    background-color: #008fff;
    cursor: pointer;
  }
  div .active a{
    color: aliceblue;
  }
  div a{
    color: #2c3f50;
  }
</style>