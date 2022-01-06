<template>
  <div class="calc">
      <div class="main">
          <label for="op1"><input type="number" id="op1" v-model.number="op1"></label>
          <label for="op2"><input type="number" id="op2" v-model.number="op2"></label>
          = {{ result }}
      </div>
      <div class="error" v-show="error">
        Ошибка: {{ error }}
      </div>
      <div class="operations">

        <button
          v-for="button of buttons"
          v-bind:key="button"
          v-bind:disabled="!op1 || !op2"
          @click="calculate(button)">
          {{ button }}
        </button>
      </div>

      <div class="keyboard">
        <label>
          <input v-model="showCalc" type="checkbox"> Отобразить экранную клавиатуру
        </label>
        <div v-if="showCalc" class="keyboard__buttons">
          <button
          v-for="number in numbers"
          class="keyboard__button"
          v-bind:key="number"
          @click="keyboardHandler(checkedOperand, number)"
          >
            {{ number }}
          </button>
          <div class="keyboard__operands">
          <label>
            <input type="radio" name="operand" v-model="checkedOperand" value="1"> Операнд 1
          </label>
          <label>
            <input type="radio" name="operand" v-model="checkedOperand" value="2"> Операнд 2
          </label>
        </div>
      </div>
        </div>
  </div>
</template>

<script>
export default {
  name: 'Calc',
  data: () => ({
    result: 0,
    op1: null,
    op2: null,
    error: '',
    buttons: ['+', '-', '*', '/', '^', '%'],

    numbers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 'Delete'],
    keyboardOp1: [],
    keyboardOp2: [],
    showCalc: true,
    checkedOperand: 1
  }),
  methods: {
    sum () {
      this.result = this.op1 + this.op2
    },

    diff () {
      this.result = this.op1 - this.op2
    },

    multi () {
      this.result = this.op1 * this.op2
    },

    div () {
      this.result = this.op1 / this.op2
    },

    pow() {
      const { op1, op2 } = this;
      this.result = Math.pow(op1, op2);
    },

    trunc() {
      const { op1, op2 } = this;
      this.result = Math.trunc(op1 / op2);
    },

    calculate (op) {
      switch (op) {
        case '+': this.sum(); break;
        case '-': this.sub(); break;
        case '/': this.div(); break;
        case '*': this.mult(); break;
        case '^': this.pow(); break;
        case '%': this.trunc(); break;
      }
    },

    keyboardHandler (checkedOperand, button) {
      if (+checkedOperand === 1) {
        if (button === 'Delete') {
          this.keyboardOp1.pop()
        } else {
          this.keyboardOp1.push(button.toString())
        }
        this.op1 = +this.keyboardOp1.join('')
      } else if (+checkedOperand === 2) {
        if (button === 'Delete') {
          this.keyboardOp2.pop()
        } else {
          this.keyboardOp2.push(button.toString())
        }
        this.op2 = +this.keyboardOp2.join('')
      }
    }
  }
}
</script>

<style scope lang="scss">
#op1 {
  margin-right: 15px;
}

.main {
  margin-bottom: 20px;
}

button {
  margin-right: 15px;
}

.keyboard {
  margin-top: 30px;

  &__buttons {
    margin-top: 15px;
  }

  &__button {
    margin-right: 5px;
  }

  &__operands {
    margin-top: 15px;
  }
}
</style>