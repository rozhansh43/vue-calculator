<template>
  <div>
    <div class="calculator">
      <input type="text" v-model="result">

      <div class="buttons">
        <Button :x="x" @myfunction="functions(x)"  v-for="x in numbers" :key="x" />
      </div>
    </div>
  </div>
</template>

<script>
import Button from '@/components/Button'

export default {
  components: {
    Button,
  },
  name: 'Calculator',
  data() {
    return {
      value: '',
      numbers: ['C','*','/','-',7,8,9,'+',4,5,6,'%',1,2,3,'=',0,'.'],
      operator: '',
      newvalue: '',
      newoperator: '',
    }
  },
  methods: {
    functions (x) {
      if(!isNaN(x) || x === '.') {
        this.value += x + '';
      }
      if (x === 'C') {
        this.value = '';
      }
      if (['/','*','-','+','%'].includes(x)) {
        this.operator = x;
        if(this.operator.length > 1) {
        this.newoperator = this.operator
          this.operator = ''
          this.value += this.newoperator
        }else {
          this.value += this.operator
        }
      }

      if (x === '=') {
        this.value = eval(
          this.newvalue + this.operator + this.value 
        );
        this.newvalue = '';
        this.operator = '';
      }
    }
  },
  computed: {
    result () {
      var result = this.value + this.operator + this.newvalue 

      if (result == 0) {
        return 0
      }else {
        return result
      }
    } 
  }
}
</script>