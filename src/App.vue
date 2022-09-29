<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <questions v-if="questionsAnswered < questions.length" :questions="questions" :questionsAnswered="questionsAnswered" @question-answered="questionAnswered" />
      <result v-else :results="results" :totalCorrect="totalCorrect" />
    </transition>

    <button type="button" class="reset-btn" @click.prevent="reset" v-if="questionsAnswered === questions.length">Reset</button>
  </div>
</template>

<script>
import Questions from "./components/Questions.vue";
import Result from "./components/Result.vue";

export default {
  name: "App",
  components: {
    Questions,
    Result,
  },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: "What is 2 + 2?",
          answers: [
            {
              text: "4",
              is_correct: true,
            },
            {
              text: "3",
              is_correct: false,
            },
            {
              text: "Fish",
              is_correct: false,
            },
            {
              text: "5",
              is_correct: false,
            },
          ],
        },
        {
          q: 'How many letters are in the word "Banana"?',
          answers: [
            {
              text: "5",
              is_correct: false,
            },
            {
              text: "7",
              is_correct: false,
            },
            {
              text: "6",
              is_correct: true,
            },
            {
              text: "12",
              is_correct: false,
            },
          ],
        },
        {
          q: "Find the missing letter: C_ke",
          answers: [
            {
              text: "e",
              is_correct: false,
            },
            {
              text: "a",
              is_correct: true,
            },
            {
              text: "i",
              is_correct: false,
            },
          ],
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "Try again!",
          desc: "Do a little more studying and you may succeed!",
        },
        {
          min: 3,
          max: 3,
          title: "Wow, you're a genius!",
          desc: "Studying has definitely paid off for you!",
        },
      ],
    };
  },
  methods: {
    questionAnswered(is_correct) {
      if (is_correct) {
        this.totalCorrect++;
      }

      this.questionsAnswered++;
    },
    reset() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap");
* {
  box-sizing: border-box;
}
body {
  font-size: 20px;
  font-family: sans-serif;
  padding-top: 20px;
  background: #e6ecf1;
  font-family: "Poppins", sans-serif;
  background: linear-gradient(180deg, #3b1684 0%, #0a1524 57.09%);
  height: 100vh;
}

.ctr {
  margin: 0 auto;
  max-width: 991px;
  width: 100%;
  box-sizing: border-box;
  position: relative;
}
.questions-ctr {
  position: relative;
  width: 100%;
  border-radius: 20px;
}
.question {
  width: 100%;
  padding: 20px;
  font-size: 2rem;
  font-weight: 600;
  text-align: center;
  color: #fff;
  box-sizing: border-box;
  margin-bottom: 3rem;
}
.single-question {
  position: relative;
  width: 100%;
}
.answers {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
}
.answer {
  border: 1px solid #8e959f;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 1rem;
  font-size: 18px;
  width: 100%;
  background-color: #fff;
  transition: 0.2s linear all;
}
.answer span {
  display: inline-block;
  margin-left: 5px;
  font-size: 0.75em;
  font-style: italic;
}
.progress {
  height: 50px;
  margin-top: 10px;
  background-color: #ddd;
  position: relative;
  border-radius: 100px;
  margin-bottom: 2rem;
}

.bar {
  height: 50px;
  background: linear-gradient(145deg, #dea720 4.09%, #ffcc50 4.1%, #ffb505 60.38%);
  transition: all 0.3s linear;
  border-radius: 100px;
}
.status {
  position: absolute;
  top: 15px;
  left: 0;
  text-align: center;
  color: #fff;
  width: 100%;
}
.answer:not(.is-answered) {
  cursor: pointer;
}
.answer:not(.is-answered):hover {
  background: linear-gradient(360deg, #dea720 4.09%, #ffcc50 4.1%, #ffb505 60.38%);
  color: #fff;
}
.ctr {
  overflow: hidden;
  height: 90vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.title {
  width: 100%;
  padding: 10px;
  font-size: 3rem;
  font-weight: bold;
  text-align: center;
  color: #fff;
  box-sizing: border-box;
}
.desc {
  padding: 20px;
  font-size: 18px;
  width: 100%;
  transition: 0.4s linear all;
  text-align: center;
  color: white;
}
.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 0.3s linear;
}
.fade-leave-active {
  transition: all 0.3s linear;
  opacity: 0;
  position: absolute;
}
.fade-leave-to {
  opacity: 0;
}

.reset-btn {
  background-color: #ff6372;
  border-radius: 12px;
  border: 0;
  font-size: 22px;
  color: #fff;
  padding: 10px 40px;
  margin: 10px auto;
  display: block;
  cursor: pointer;
}

.result {
  width: 100%;
}

.reset-btn:active,
.reset-btn:focus,
.reset-btn:hover {
  border: 0;
  outline: 0;
}
</style>
