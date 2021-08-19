<template>
  <div id="mental_calculation" class="m-outer">
    <h1>Mental calculation</h1>
    <p>Click on the question or press ENTER to get answer.</p>
    <p>Click on the NEW button or press RIGHT to get new questions.</p>
    <div class="m-main">
      <div v-if="!showAnswer" class="main-content" @click="toggleClick">
        {{ firstNumber }} {{ operator }} {{ secondNumber }}
      </div>
      <div v-if="showAnswer" class="main-content" @click="toggleClick">
        {{ answer }}
      </div>
      <button class="main-button" @click="nextQuestion">&gt;</button>
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
  flex-wrap: wrap;
  justify-content: space-around;
  align-items: center;
}
.main-content {
  font-size: 92px;
}
.main-button {
  padding: 12px;
  font-size: 24px;
}
@media (max-width: 480px) {
  .main-content {
    font-size: 52px;
  }
}
</style>
