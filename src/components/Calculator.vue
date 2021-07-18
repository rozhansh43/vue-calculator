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
        if (this.value == this.operator) {
          this.value = this.operator
        }else {
          this.value += this.operator;
          this.operator = ''
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
      var result = this.value

      if (result == 0) {
        return 0
      }else {
        return result
      }
    } 
  }
}
</script>