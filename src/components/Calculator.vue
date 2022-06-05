<template>
  <h2>VueJS 3 Calculator</h2>
  <div class="p-3" style="max-width: 400px; margin: 50px auto; background: #234">
    <div class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white bg-vue-dark">
      {{ calculatorValue || 0 }}
    </div>

    <!-- Calculator buttons -->
    <div class="row no-gutters">
      <div class="col-3" :class="{'col-6': [0].includes(n)}" v-for="n in calculatorElements" :key="n">
        <div class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class "
             :class="{'bg-vue-green': ['C','*','/','-','+','%','='].includes(n)}"
             @click="action(n)">
          {{n}}
        </div>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'CalculatorComponent',
  props: {
    msg: String
  },
  data() {
    return {
      calculatorValue: '',
      calculatorElements: ['C','*','/','-',7,8,9,'+',4,5,6,'%',1,2,3,'=',0,'.'],
      operator: null,
      previousCalculatorValue: '',
    }
  },
  methods: {
    action(n){
      /* Append value */
      if(!isNaN(n) || n === '.'){
        this.calculatorValue += n + '';
      }
      /* Clear value */
      if(n === 'C'){
        this.calculatorValue = '';
      }
      /* Percentage */
      if(n === '%'){
        this.calculatorValue = this.calculatorValue / 100 + '';
      }
      /* Operators */
      if(['/','*','-','+'].includes(n)){
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = '';
      }
      /* Calculate result using the eval function */
      if(n === '='){
        this.calculatorValue = eval(
            this.previousCalculatorValue + this.operator + this.calculatorValue
        );
        this.previousCalculatorValue = '';
        this.operator = null;
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.bg-vue-dark {
  background: #D56F3E;
}
.hover-class:hover {
  cursor: pointer;
  background: #241623;
}
.bg-vue-green {
  background: #241623;
}
</style>
