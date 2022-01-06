<template>
  <div>
    <div class="main">
      <input type="number" v-model.number="op1">
      <input type="number" v-model.number="op2">
      = {{ result }} <br/>
      Fibonacci-1 = {{ fib1 }} <br/>
      Fibonacci-2 = {{ fib2() }}
    </div>
    <!-- <div class="error" v-if="error">
      Ошибка: {{ error }}
    </div> -->
    <div class="error" v-show="error">
      Ошибка: {{ error }}
    </div>
    <!-- <div class="messages">
      <template v-if="result < 0">Отрицательный результат</template>
      <template v-else-if="result < 100">Результат в первой сотне</template>
      <template v-else>Простой результат</template>
    </div> -->
    <!-- <div class="keyboard">
      <button @click="calculate('+')">+</button>
      <button @click="calculate('-')">-</button>
      <button @click="calculate('/')">/</button>
      <button @click="calculate('*')">*</button>
      <button @click="calculate('^')">^</button>
      <button @click="calculate('%')">%</button>
    </div> -->
    <div class="keyboard">
      <button 
      v-for="operator in operators" 
      @click="calculate(operator)" 
      :title="operator"
      :key="operator"
      >
      {{ operator }}
      </button>
    </div>

    <div class="logs">
      {{ logs }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
      op1: 0,
      op2: 0,
      result: 0,
      error: '',
      operators: ['+', '-', '/', '*', '^', '%'],
      logs: {},
    }
  },
  methods: {
    sum() {
      const { op1, op2 } = this;
      this.result = op1 + op2;
    },
    sub() {
      const { op1, op2 } = this;
      this.result = op1 - op2;
    },
    div() {
      const { op1, op2 } = this;
      
      if (op2 === 0) this.error = 'На ноль делить нельзя!';
      else this.result = op1 / op2;
    },
    mult() {
      const { op1, op2 } = this;
      this.result = op1 * op2;
    },
    pow() {
      const { op1, op2 } = this;
      this.result = Math.pow(op1, op2);
    },
    trunc() {
      const { op1, op2 } = this;
      this.result = Math.trunc(op1 / op2);
    },
    calculate(operation) {
      this.error = '';
      const { op1, op2 } = this;
      switch (operation) {
        case '+': this.sum(); break;
        case '-': this.sub(); break;
        case '/': this.div(); break;
        case '*': this.mult(); break;
        case '^': this.pow(); break;
        case '%': this.trunc(); break;
      }

      // this.logs[Date.now()] = `${op1} ${operation} ${op2}`;
      // this.logs = { ...this.logs, [Date.now()]: `${op1} ${operation} ${op2}` };
      // Vue.set();
      this.$set(this.logs, Date.now(), `${op1} ${operation} ${op2}`);
    },

    fib(n) {
      return n <= 1 ? n : this.fib(n - 1) + this.fib(n - 2);
    },

    fib2() {
      console.log('method');
      const { op2 } = this;

      return this.fib(op2);
    },
  },

  computed: {
    fib1() {
      console.log('computed');
      const { op1 } = this;

      return this.fib(op1);
    },
    // fib2() {
    //   console.log('computed');
    //   const { op2 } = this;
    //
    //   return this.fib(op2);
    // },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
button {
  background-color: pink;
  color: black;
  border: 1px solid #696969;
  padding: 5px 13px;
  margin: 10px 3px;
  font-size: 16px;
}
</style>