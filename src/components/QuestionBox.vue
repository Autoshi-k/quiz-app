<script>
import { shuffle } from 'lodash';
export default {
  props: {
    question: Object,
    next: Function
  },
  data() {
    return {
      selectedAnswer: null,
      submitted: false
    }  
  },
  methods: {
    selectAnswer(index) {
      this.selectedAnswer = index
    },
    handleSubmit() {
      console.log('submitted')
      this.submitted = true
    }
  },
  computed: {
    answers() {
      let results = [];
      for (let index in this.question.incorrect_answers) {
        results.push({ answer: this.question.incorrect_answers[index], correct: false })
      }
      results.push({ answer: this.question.correct_answer, correct: true })
      results = shuffle(results)
      return results
    }
  },
  watch: {
    question() {
      this.selectedAnswer = null
      this.submitted = false
      this.shuffleAnswers()
    }
  }
}
</script>


<template>
  <div class="wrapper">
    <div class="question-box">
      <h3>{{ question.question }}</h3>
      <ul class="answers">
        <li 
          v-for="(answer, index) in answers" 
          :key="index"
          @click="selectAnswer(index)"
          :class="[
            index === selectedAnswer ? 'selected': '', 
            submitted ? answer.correct ? 'correct' : 'incorrect' : ''
          ]"
          >
          {{answer.answer}}
        </li>
      </ul>
      <button class="btn-pink" @click="handleSubmit()">submit</button>
      <button class="btn-pink grey" @click="next">next question</button>
    </div>
  </div>
</template>

<style scoped>
  .question-box {
    width: 500px;
    margin: 0 auto;
    text-align: center;
  }

  .wrapper {
    flex: 1;
    padding: 3rem;
  }

  .question-box h3 {
    padding-bottom: .5rem;
    text-align: left;
    text-transform: capitalize;
  }

  .question-box button {
    width: 100%;
  }

  .question-box ul {
    list-style: none;
    padding: 0;
  }

  .question-box ul li {
    height: 2.5rem;
    background-color: rgb(255, 235, 238);
    border-radius: .2rem;
    margin-bottom: .5rem;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
  }

  .question-box ul li:hover {
    background-color: rgb(255, 182, 193);
    color: rgb(246, 236, 236);
    filter: drop-shadow(0 3px 10px rgb(238, 238, 238));
  }

  .question-box button {
    height: 3rem;
  }

  .question-box button.grey {
    background-color: transparent;
    color: rgb(100, 100, 100);
    margin-top: .5rem;
    filter: none;
  }

  .question-box button.grey:hover {
    background-color: transparent;  
    color: black;
  }

  .selected {
    background-color: rgb(177, 108, 131) !important;
  }
  .selected.incorrect {
    background-color: rgb(228, 62, 62) !important;
  }
  .correct {
    background-color: rgb(131, 221, 154) !important;
  }
</style>