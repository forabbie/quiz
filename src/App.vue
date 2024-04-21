<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <TheQuestions
        v-if="questionsAnswered < questions.length"
        :questions="questions"
        :questionsAnswered="questionsAnswered"
        @question-answered="questionAnswered"
      />
      <TheResult v-else :results="results" :totalCorrect="totalCorrect" />
    </transition>
    <button
      type="button"
      class="reset-btn"
      @click.prevent="onReset"
      v-if="questionsAnswered === questions.length"
    >
      Reset
    </button>
  </div>
</template>

<script setup>
import TheQuestions from '@/components/TheQuestions.vue'
import TheResult from '@/components/TheResult.vue'
import { ref } from 'vue'

let questionsAnswered = ref(0)
let totalCorrect = ref(0)
const questions = [
  {
    q: 'What is 2 + 2?',
    answers: [
      {
        text: '4',
        is_correct: true
      },
      {
        text: '3',
        is_correct: false
      },
      {
        text: 'Fish',
        is_correct: false
      },
      {
        text: '5',
        is_correct: false
      }
    ]
  },
  {
    q: 'How many letters are in the word "Banana"?',
    answers: [
      {
        text: '5',
        is_correct: false
      },
      {
        text: '7',
        is_correct: false
      },
      {
        text: '6',
        is_correct: true
      },
      {
        text: '12',
        is_correct: false
      }
    ]
  },
  {
    q: 'Find the missing letter: C_ke',
    answers: [
      {
        text: 'e',
        is_correct: false
      },
      {
        text: 'a',
        is_correct: true
      },
      {
        text: 'i',
        is_correct: false
      }
    ]
  }
]
const results = [
  {
    min: 0,
    max: 2,
    title: 'Try again!',
    desc: 'Do a little more studying and you may succeed!'
  },
  {
    min: 3,
    max: 3,
    title: "Wow, you're a genius!",
    desc: 'Studying has definitely paid off for you!'
  }
]
const questionAnswered = (is_correct) => {
  if (is_correct) {
    totalCorrect.value++
  }
  questionsAnswered.value++
}

const onReset = () => {
  questionsAnswered.value = 0
  totalCorrect.value = 0
}
</script>
