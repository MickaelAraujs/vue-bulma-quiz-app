<template>
  <div id="app">
    <Header 
      :correctAnswers="correctAnswers"
      :totalQuestions="totalQuestions"
    />

    <div class="columns">
      <QuestionBox
        class="column is-half is-offset-3"
        v-if="questions.length > 0"
        :questionData="questions[questionIndex]"
        :next="handleNext"
        :handleCorrectAnswer="handleCorrectAnswer"
      />
    </div>
  </div>
</template>

<script>
import Header from './components/Header';
import QuestionBox from './components/QuestionBox';

export default {
  name: 'App',

  components: {
    Header,
    QuestionBox,
  },

  data() {
    return {
      questions: [],
      questionIndex: 0,

      correctAnswers: 0,
      totalQuestions: 0
    }
  },

  methods: {
    handleNext() {
      const finalQuestionIndex = this.questions.length - 1;

      if (this.questionIndex >= 0 && this.questionIndex < finalQuestionIndex) {
        this.questionIndex++;
      }
    },

    handleCorrectAnswer(isCorrect) {
      if (isCorrect) {
        this.correctAnswers++;
      }
    }
  },

  async mounted() {
    const questionsResponse = await fetch('https://opentdb.com/api.php?amount=10&category=29&type=multiple', {
      method: 'GET'
    })
    .then(apiResponse => apiResponse.json())
    .catch(err => console.warn(err));

    const { results } = questionsResponse;
    
    this.questions = results;
    this.totalQuestions = results.length;
  }
  
}
</script>
