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
      questionIndex: 0
    }
  },
  methods: {
    next() {
      this.questionIndex++;
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
      <Header />
      <QuestionBox 
        v-if="questions.length"
        :question="questions[questionIndex]" 
        :next="next"/>
    </div>
</template>

<style>
@import '@/assets/base.css';

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

.btn-pink {
  background-color: palevioletred;
  color: white;
  font-weight: 600;
  letter-spacing: 2px;
  text-transform: uppercase;
  border-radius: .2rem;
  border: none;
  filter: drop-shadow(0 3px 10px rgb(238, 238, 238));
}

.btn-pink:hover {
  background-color: rgb(204, 81, 122);
  filter: drop-shadow(0 3px 10px rgb(212, 212, 212));
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
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
