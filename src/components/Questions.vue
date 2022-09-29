<template>
  <div class="questions-ctr">
    <div class="progress">
      <div class="bar" :style="{ width: `${(questionsAnswered / questions.length) * 100}%` }"></div>
      <div class="status">{{ questionsAnswered }} out of {{ questions.length }} questions answered</div>
    </div>
    <transition-group name="fade">
      <div class="single-question" v-for="(question, qi) in questions" :key="question.q" v-show="questionsAnswered === qi">
        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <div v-for="answer in question.answers" :key="answer.text" class="answer" @click.prevent="selectAnswer(answer.is_correct)">
            {{ answer.text }}
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  props: ["questions", "questionsAnswered"],
  emits: ["question-answered"],
  methods: {
    selectAnswer(is_correct) {
      this.$emit("question-answered", is_correct);
    },
  },
};
</script>
