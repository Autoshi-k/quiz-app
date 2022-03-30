<script>
import Header from './components/Header.vue';
import QuestionBox from './components/QuestionBox.vue';

export default {
  name: 'app',
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      questions: [],
      questionIndex: 0,
      score: 0
    }
  },
  methods: {
    next() {
      this.questionIndex++;
    },
    updateScore() {
      this.score++
    }
  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple', {
      method: 'get'
    })
    .then(res => res.json())
    .then(data => this.questions = data.results)
  }
}
</script>

<template>
    <div class="wrapper">
      <Header 
        v-if="questions.length"
        :length="questions.length"
        :score="score"
      />
      <QuestionBox 
        v-if="questions.length"
        :question="questions[questionIndex]" 
        :next="next"
        :updateScore="updateScore"
        />
    </div>
</template>

<style>
@import '@/assets/base.css';

#app {
  max-width: 1280px;
  margin: 0 auto;
  /* padding: 2rem; */

  font-weight: normal;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

.btn-pink {
  width: 90vw;
  max-width: 100%;
  background-color: palevioletred;
  color: white;
  font-weight: 600;
  letter-spacing: 2px;
  text-transform: uppercase;
  border-radius: .2rem;
  border: none;
  filter: drop-shadow(0 3px 10px rgb(238, 238, 238));
  cursor: pointer;
}

.btn-pink:hover {
  background-color: rgb(204, 81, 122);
  filter: drop-shadow(0 3px 10px rgb(212, 212, 212));
}

@media (min-width: 1024px) {
  body {
    display: flex;
  }

  #app {
    padding: 0;
    margin: 0;
  }

  .wrapper { 
    display: flex;
    flex-direction: column;
    height: 100vh;
    width: 100vw;
  }
}
</style>
