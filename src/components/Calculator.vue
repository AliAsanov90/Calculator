<template>
  <div class="calculator">
    <div class="btn display">{{ current }}</div>
    <div @click="clear" class="btn gray-button">AC</div>
    <div @click="negative" class="btn gray-button">+/-</div>
    <div class="btn gray-button">%</div>
    <div class="btn operator">/</div> 
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div class="btn">.</div>
    <div class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
      current: '0'
    }
  },
  methods: {
    clear() {
      this.current = '0'
    },
    append(number) {
      if (this.current.indexOf('0') === 0) {
        this.current = this.current.substring(1)
      }
      this.current = `${this.current}${number}`
    },
    negative() {
      if (this.current.indexOf('-') === -1) {
        this.current = `-${this.current}`
      } else {
        this.current = this.current.substring(1)
      }
    }
  }
}
</script>

<style scoped>
  .calculator {
    width: 350px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: 70px;
    grid-gap: 15px;
    padding: 20px;
    border-radius: 10px;
    background-color: black;
  }

  .btn {
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 30px;
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
    font-size: 60px;
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
