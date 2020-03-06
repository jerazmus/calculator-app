<template>
    <div id="app">
      <div class="btn result">{{current}}</div>
      <div @click="clear" class="btn top-method">AC</div>
      <div @click="sqrt" class="btn top-method">√</div>
      <div @click="sign" class="btn top-method">+/-</div>
      <div @click="divide" class="btn right-method">÷</div>
      <div @click="click('7')" class="btn">7</div>
      <div @click="click('8')" class="btn">8</div>
      <div @click="click('9')" class="btn">9</div>
      <div @click="multi" class="btn right-method">x</div>
      <div @click="click('4')" class="btn">4</div>
      <div @click="click('5')" class="btn">5</div>
      <div @click="click('6')" class="btn">6</div>
      <div @click="decrease" class="btn right-method">-</div>
      <div @click="click('1')" class="btn">1</div>
      <div @click="click('2')" class="btn">2</div>
      <div @click="click('3')" class="btn">3</div>
      <div @click="add" class="btn right-method">+</div>
      <div @click="zero" class="btn zero">0</div>
      <div @click="dot" class="btn">.</div>
      <div @click="equal" class="btn right-method">=</div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorUsed: false,
    }
  },
  methods: {
    click(number) {
      if(this.operatorUsed) {
        this.current = ''
        this.operatorUsed = false
      }
      this.current = `${this.current}${number}`
    },
    clear() {
      this.current = ''
      this.previous = null
    },
    setPrevious() {
      this.previous = this.current
      this.operatorUsed = true;
    },
    equal() {
      if(this.previous !== null) {
      this.current = this.operator(parseFloat(this.previous), parseFloat(this.current))
      this.previous = null
      }
    },
    add() {
      this.operator = (a,b) => a+b
      this.setPrevious()
    },
    decrease() {
      this.operator = (a,b) => a-b
      this.setPrevious()
    },
    divide() {
      this.operator = (a,b) => a/b
      this.setPrevious()
    },
    multi() {
      this.operator = (a,b) => a*b
      this.setPrevious()
    },
    sqrt() {
      this.current = Math.sqrt(this.current)
    },
    sign() {
      if(this.current[0] === '-') {
        this.current = this.current.slice(1)
      } else {
        this.current = `-${this.current}`
      }
    },
    dot() {
      if(this.current.indexOf('.') === -1) {
        this.click('.')
      }
    },
    zero() {
      if(this.current.charAt(0) !== '0' || this.current.charAt(1) === '.') {
        this.click('0')
      }
    }
  }
}
</script>
