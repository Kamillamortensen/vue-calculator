<template>
  <div id="app" class='grid-container'>
      <div class='calculator-container'>
        <calculator @new-calculation='updateCalculationLog($event)'></calculator>
      </div>
      <div class='calculator-logg-container'>
        <calculatorLog :calculations='calculations'></calculatorLog>
      </div>
  </div>
</template>

<script>
import calculator from './components/calculator.vue'
import calculatorLog from './components/calculatorLog.vue'

export default {
  name: 'App',
  components: {
    calculator,
    calculatorLog
  },
  data() {
    return{
      calculations: [  
        ]
    }
  },
  methods: {
    updateCalculationLog(info){
      const newCalc = {
        calculation: info.calculation,
        answer: info.answer
      }
      this.calculations.unshift(newCalc)
    }
  }
}
</script>

<style>

@import './assets/grid.css';
@import './assets/styles.css';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>


