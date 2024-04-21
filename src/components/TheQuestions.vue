<template>
  <div class="questions-ctr">
    <div class="progress">
      <div class="bar" :style="{ width: `${(questionsAnswered / questions.length) * 100}%` }"></div>
      <div class="status">
        {{ questionsAnswered }} out of {{ questions.length }} questions answered
      </div>
    </div>
    <transition-group name="fade">
      <div
        class="single-question"
        v-for="(question, i) in questions"
        :key="i"
        v-show="questionsAnswered === i"
      >
        <div class="question">{{ question.q }}</div>
        <div
          class="answers"
          v-for="(answer, i) in question.answers"
          :key="i"
          @click.prevent="selectAnswer(answer.is_correct)"
        >
          <div class="answer">{{ answer.text }}</div>
        </div>
      </div>
    </transition-group>
  </div>
</template>
<script setup>
defineProps({
  questions: Object,
  questionsAnswered: Number
})

const emits = defineEmits(['question-answered'])

const selectAnswer = (is_correct) => {
  emits('question-answered', is_correct)
  console.log('asd: ', is_correct)
}
</script>
<style scoped></style>
