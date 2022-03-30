<script>
export default {
  props: {
    question: Object,
    next: Function
  },
  data() {
    return {
      results: []
    }  
  },
  computed: {
    answers() {
      const results = [];
    for (let index in this.question.incorrect_answers) {
      results.push({ answer: this.question.incorrect_answers[index], correct: false })
    }
    results.push({ answer: this.question.correct_answer, correct: true })
    console.log(results)
    return results
    }
  }
}
</script>


<template>
  <div class="wrapper">
    <div class="question-box">
      <h3>{{ question.question }}</h3>
      <ul class="answers">
        <li v-for="(answer, index) in answers" :key="index">{{answer.answer}}</li>
      </ul>
      <button class="btn-pink">submit</button>
      <button class="btn-pink grey" @click="next">next question</button>
    </div>
  </div>
</template>

<style scoped>
  .question-box {
    width: 500px;
    margin: auto auto;
    text-align: center;
  }

  .wrapper {
    flex: 1;
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
</style>