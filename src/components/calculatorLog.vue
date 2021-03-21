<template> 
<div>
  <button class='log-button' id='log-button' @click='updateLogDisplay'>show log</button>
  <div class='log' v-if="showLog" >
    <ul id="example-1">
      <li v-for="calculation in this.calculations" :key="calculation">  
        {{ calculation.calculation + " = " + calculation.answer }}
      </li>
    </ul>
  </div>
</div>
</template>


<script>
  export default {
     props: {
      calculations: {
        type: Array
      },
      test: {
        type: Boolean
      }
    },
    data() {
      return {
        showLog: false,
      }
    },
    methods: { //update log, //show log, //hide log 
      updateLogDisplay(){
        if(this.showLog){
          this.showLog = false
          document.getElementById('log-button').innerHTML = 'show log'
        }
        else{
          this.showLog = true
          document.getElementById('log-button').innerHTML = 'hide log'
        }
      }
    },
    computed: {
    }
  }
</script>