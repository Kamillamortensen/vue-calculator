<template> 
    <div class="calculator">
    <div class='answer-display'>
      <h1>{{ answerDisplay }}</h1>
    </div>
    <div class='button-container'>
      <div class="button-container-row4">
        <button class='numberButton' @click='updateAnswerDisplay(7)'>7</button>
        <button class='numberButton' @click='updateAnswerDisplay(8)'>8</button>
        <button class='numberButton' @click='updateAnswerDisplay(9)'>9</button>
        <button @click='updateAnswerDisplay("/")'>/</button>
      </div>
      <div class='button-container-row3'>
        <button class='numberButton' @click='updateAnswerDisplay(4)'>4</button>
        <button class='numberButton' @click='updateAnswerDisplay(5)'>5</button>
        <button class='numberButton' @click='updateAnswerDisplay(6)'>6</button>
        <button @click='updateAnswerDisplay("*")'>*</button>
      </div>
      
      <div class='button-container-row2'>
        <button class='numberButton' @click='updateAnswerDisplay(1)'>1</button>
        <button class='numberButton' @click='updateAnswerDisplay(2)'>2</button>
        <button class='numberButton' @click='updateAnswerDisplay(3)'>3</button>
        <button @click='updateAnswerDisplay("-")'>-</button>
      </div>
      <div class='button-container-row1'>
        <button class='numberButton' @click='updateAnswerDisplay(0)'>0</button>
        <button @click='updateAnswerDisplay(".")'>.</button>
        <button @click='doCalculation()'>=</button>
        <button @click='updateAnswerDisplay("+")'>+</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    data() {
      return {
          answerDisplay: 'hello',
          answerShowing: false,
      }
    },
    methods: {
        updateAnswerDisplay(value){
          //nytt regnestykke?
          if(this.answerDisplay == 'hello' || this.answerShowing == true){
            //hvis symbol, gi beskjed om å starte med tall 
            if(value ==  "+" || value == "-" || value == "*" || value == "/" ){
              alert("start regnestykke med tall!") 
              return
            }
            this.answerDisplay = ''
            this.answerShowing = false 
          }
          //sjekke om vi evt får flere regnetegn på rad
          if((value ==  "+" || value == "-" || value == "*" || value == "/")  && (this.lastChar == "+" || this.lastChar == "-" || this.lastChar == "*" || this.lastChar == "/")){
            alert("regnetegn må etterfølges av tall!") 
            return
          } 
          this.answerDisplay += value; 
        },
        doCalculation(){
          //hvis siste char er symbol fjernes det før kalkulasjon
          if(this.lastChar == "+" || this.lastChar == "-" || this.lastChar == "*" || this.lastChar == "/" ){
            this.answerDisplay = this.answerDisplay.slice(0, this.answerDisplay.length-1); 
          }
          const ans = this.calculation
          this.updateCalculatorLog(ans)
          this.answerDisplay = ans
          this.answerShowing = true 
        },
        updateCalculatorLog(ans) {
          this.$emit('new-calculation', {
            calculation: this.answerDisplay,
            answer: ans
        })
      }
    },
    computed: {
        calculation() {
            return eval(this.answerDisplay).toPrecision(4)
        },
        lastChar() {
            return this.answerDisplay.charAt(this.answerDisplay.length-1)
        }
    }
}
</script>




  