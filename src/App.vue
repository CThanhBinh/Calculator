<template>
  <h1>Calculator</h1>
    <div class="output">
      <div class="outputCalc">{{ result || num2 + sign + num1 || 0 }}</div>
    </div>
    <div class="buttons">
      <div class="button" v-for="item in btnArr" @click="num(item)" :key="item">
        {{ item }}
      </div>
    </div>
    <div class="buttons2">
      <div class="button" @click="clear">
        C
      </div>
      <div class="button" v-for="operator in btnOperator" @click="action(operator)" :key="operator">
        {{ operator }}
      </div>
      <div class="button" @click="expression">
        =
      </div>
    </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      result: '',
      sign: '',
      num1: '',
      num2: '',
      operator: '',
      btnOperator: [
        '*', '/', '-', '+'
      ],
      btnArr: [
        '7', '8', '9',
        '4', '5', '6',
        '1', '2', '3',
        '0', '.', '%'
      ]
    }
  },
  methods: {
    clear () {
      this.num1 = ''
      this.num2 = ''
      this.operator = ''
      this.result = ''
      this.sign = ''
    },
    num (item) {
      if (!isNaN(item) || item === '.') {
        this.num1 += item
      }
      if (item === '%') {
        if (this.num1 || this.num2 === '') {
          this.num1 = ''
        } else {
          this.num1 = this.num1 / 100
        }
      }
    },
    action (operator) {
      if (operator === '*') {
        this.operator = (a, b) => a * b
      }
      if (operator === '/') {
        this.operator = (a, b) => a / b
      }
      if (operator === '-') {
        this.operator = (a, b) => a - b
      }
      if (operator === '+') {
        this.operator = (a, b) => a + b
      }
      this.result = ''
      this.sign = ' ' + operator + ' '
      this.num2 = this.num1
      this.num1 = ''
    },
    expression () {
      const a = Number(this.num2)
      const b = Number(this.num1)
      this.num1 = this.result = this.operator(a, b)
    }
  }
}
</script>

<style>
h1 {
  margin-top: 100px;
  text-align: center;
}

.output {
  font-size: 2em;
  text-align: right;
  background-color: antiquewhite;
  width: min(300px, 70%);
  margin: 10px auto 0;
  padding: 10px;
  border: 0.5px solid rgb(255, 198, 124);
  border-radius: 4px 4px 0 0;
  box-shadow: 2.8px 2.8px 2.2px rgba(0, 0, 0, 0.008),
    6.7px 6.7px 5.3px rgba(0, 0, 0, 0.012),
    12.5px 12.5px 10px rgba(0, 0, 0, 0.015),
    22.3px 22.3px 17.9px rgba(0, 0, 0, 0.018),
    41.8px 41.8px 33.4px rgba(0, 0, 0, 0.022),
    100px 100px 80px rgba(0, 0, 0, 0.03);
}

.outputCalc {
  background-color: rgb(255, 209, 148);
  padding: 15px;
  border-radius: 3px;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: minmax(50px, auto);
  width: min(300px, 70%);
  border: 0.2px solid rgb(255, 198, 124);
  align-items: center;
  background-color: antiquewhite;
  justify-content: center;
  margin:  auto;
  padding: 10px;
  gap: 5px;
  box-shadow: 2.8px 2.8px 2.2px rgba(0, 0, 0, 0.008),
    6.7px 6.7px 5.3px rgba(0, 0, 0, 0.012),
    12.5px 12.5px 10px rgba(0, 0, 0, 0.015),
    22.3px 22.3px 17.9px rgba(0, 0, 0, 0.018),
    41.8px 41.8px 33.4px rgba(0, 0, 0, 0.022),
    100px 100px 80px rgba(0, 0, 0, 0.03);
}
.buttons2 {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: minmax(50px, auto);
  width: min(300px, 70%);
  border: 0.2px solid rgb(255, 198, 124);
  align-items: center;
  background-color: antiquewhite;
  justify-content: center;
  margin:  auto;
  padding: 10px;
  border-radius: 0 0 4px 4px;
  gap: 5px;
  box-shadow: 2.8px 2.8px 2.2px rgba(0, 0, 0, 0.008),
    6.7px 6.7px 5.3px rgba(0, 0, 0, 0.012),
    12.5px 12.5px 10px rgba(0, 0, 0, 0.015),
    22.3px 22.3px 17.9px rgba(0, 0, 0, 0.018),
    41.8px 41.8px 33.4px rgba(0, 0, 0, 0.022),
    100px 100px 80px rgba(0, 0, 0, 0.03);
}

.button {
  background-color: rgb(255, 209, 148);
  padding: 6px;
  border-radius: 3px;
  margin: 4px;
  font-size: 1.5em;
  font-weight: bold;
  color: #000;
  text-align: center;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
}

.button:hover {
  background-color: rgb(238, 167, 75);
  color: #000;
}

.operator {
  background-color: rgb(238, 167, 75);
  color: #000;
}

.operator:hover {
  background-color: rgb(255, 209, 148);
}

.MyId:hover {
  cursor: pointer;
  filter: brightness(130%);
}
</style>
