<template>
  <div class="calculator">
    <div class="btn display">{{ current || previous }}</div>
    <div @click="clear" class="btn gray-button">AC</div>
    <div @click="appendNegativeSign" class="btn gray-button">+/-</div>
    <div @click="calculatePercentage" class="btn gray-button">%</div>
    <div @click="divide" class="btn operator">/</div> 
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiply" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="subtract" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="appendFloatingPoint" class="btn">.</div>
    <div @click="getResult" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
      current: '0',
      previous: null,
      operation: null,
      equalitySignPressed: false
    }
  },
  methods: {
    clear() {
      this.current = '0'
      this.previous = null
      this.equalitySignPressed = false
    },
    append(number) {
      if (this.equalitySignPressed) return

      if ((this.current.indexOf('0') === 0) && (this.current.indexOf('.') === -1)) {
        this.current = this.current.substring(1)
      }
      this.current = `${this.current}${number}`
    },
    appendNegativeSign() {
      if (this.current.charAt(0) === '0') return

      if (this.current.indexOf('-') === -1) {
        this.current = `-${this.current}`
      } else {
        this.current = this.current.substring(1)
      }
    },
    appendFloatingPoint() {
      if (this.current.indexOf('.') === -1) {
        this.current = `${this.current}.`
      } 
    },
    calculatePercentage() {
      this.current = this.current / 100
    },
    storeAndClearCurrent() {
      this.previous = this.current
      this.current = ''
    },
    divide() {
      this.storeAndClearCurrent()
      this.operation = (a, b) => a / b
    },
    multiply() {
      this.storeAndClearCurrent()
      this.operation = (a, b) => a * b
    },
    subtract() {
      this.storeAndClearCurrent()
      this.operation = (a, b) => a - b
    },
    add() {
      this.storeAndClearCurrent()
      this.operation = (a, b) => a + b
    },
    getResult() {
      this.equalitySignPressed = true

      let maxLengthOfResult = this.previous.length > this.current.length ? 
        this.previous.length : this.current.length

      this.current = `${this.operation(parseFloat(this.previous), parseFloat(this.current))}`

      if (this.current.includes('.')) {
        // Fixing bug of incorrect result when calculating floating point numbers 
        if ((this.current.charAt(maxLengthOfResult + 1) === '9') && 
          (this.current.charAt(maxLengthOfResult - 1) !== '0')) {
          this.current = this.current
            .substring(0, maxLengthOfResult)
            .replace(
              this.current.charAt(maxLengthOfResult - 1), 
              `${parseInt(this.current.charAt(maxLengthOfResult - 1)) + 1}`
            )
        }
        if (this.current.length > maxLengthOfResult) {
          this.current = this.current.substring(0, maxLengthOfResult)
          if (this.current.endsWith('0')) {
            this.current = this.current
              .substring(0, 2)
              .padEnd(maxLengthOfResult, '1')
          }
        }
      }
    }
  }
}
</script>

<style scoped>
  .calculator {
    width: 310px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: 60px;
    grid-gap: 15px;
    padding: 20px;
    border-radius: 5px;
    background-color: black;
  }

  .btn {
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 25px;
    border: none;
    border-radius: 50%;
    color: white;
    background-color: #565656;
    cursor: pointer;
  }

  .btn:hover {
    opacity: 0.8;
  }

  .btn:active {
    opacity: 0.3;
  }

  .display {
    font-size: 40px;
    grid-column: 1 / 5;
    justify-content: flex-end;
    padding-right: 20px;
    border: none;
    border-radius: 0;
    background-color: transparent;
  }

  .zero {
    grid-column: 1 / 3;
    border-radius: 20% / 50%;
  }
  
  .operator {
    color: white;
    background-color: #F99A0B;
  }

  .gray-button {
    color: #000;
    background-color: lightgray;
  }
</style>
