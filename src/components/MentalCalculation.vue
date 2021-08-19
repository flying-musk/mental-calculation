<template>
  <div id="mental_calculation" class="m-outer">
    <h1>Mental calculation</h1>
    <p>Click on the equation or press ENTER to get answer.</p>
    <p>Click on NEW or press RIGHT to get new questions.</p>
    <div class="m-main">
      <div v-if="!showAnswer" class="main-content" @click="toggleClick">
        {{ firstNumber }} {{ operator }} {{ secondNumber }}
      </div>
      <div v-if="showAnswer" class="main-content" @click="toggleClick">
        {{ answer }}
      </div>
      <button class="main-button" @click="nextQuestion">NEW</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MentalCalculation',
  data() {
    return {
      randomNumber: Math.random(),
      showAnswer: false,
    };
  },
  computed: {
    isTimes: function () {
      return this.randomNumber < 0.75;
    },
    operator: function () {
      return this.isTimes ? '*' : '+';
    },
    firstNumber: function () {
      let number = Math.trunc(Math.random() * (this.isTimes ? 100 : 1000));
      const LEAST_NUMBER = this.isTimes ? 11 : 111;
      return number < LEAST_NUMBER ? number + LEAST_NUMBER : number;
    },
    secondNumber: function () {
      let number = Math.trunc(Math.random() * (this.isTimes ? 100 : 1000));
      const LEAST_NUMBER = this.isTimes ? 11 : 111;
      return number < LEAST_NUMBER ? number + LEAST_NUMBER : number;
    },
    answer: function () {
      return this.isTimes
        ? this.firstNumber * this.secondNumber
        : this.firstNumber + this.secondNumber;
    },
  },
  methods: {
    nextQuestion() {
      this.showAnswer = false;
      this.randomNumber = Math.random();
    },
    toggleClick() {
      this.showAnswer = !this.showAnswer;
    },
  },
  created() {
    window.addEventListener('keydown', (e) => {
      if (e.code === 'ArrowRight') {
        this.nextQuestion();
      }
      if (e.code === 'Enter') {
        this.toggleClick();
      }
    });
  },
};
</script>

<style scoped lang="scss">
.m-outer {
  display: grid;
}
.m-main {
  min-height: 60vh;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  gap: 16px;
}
.main-content {
  cursor: pointer;
  flex-grow: 1;
  align-self: stretch;
  font-size: 108px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.main-button {
  padding: 72px;
  font-size: 52px;
}
@media (max-width: 600px) {
  .main-content {
    font-size: 60px;
  }
}
</style>
