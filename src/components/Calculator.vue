<template>
  <div class="calculator">
    <div class="btn display">0</div>
    <div class="btn gray-button">AC</div>
    <div class="btn gray-button">+/-</div>
    <div class="btn gray-button">%</div>
    <div class="btn operator">/</div> 
    <div class="btn">7</div>
    <div class="btn">8</div>
    <div class="btn">9</div>
    <div class="btn operator">x</div>
    <div class="btn">4</div>
    <div class="btn">5</div>
    <div class="btn">6</div>
    <div class="btn operator">-</div>
    <div class="btn">1</div>
    <div class="btn">2</div>
    <div class="btn">3</div>
    <div class="btn operator">+</div>
    <div class="btn zero">0</div>
    <div class="btn">.</div>
    <div class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
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
