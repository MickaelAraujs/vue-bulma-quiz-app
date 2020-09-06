<template>
  <div id="app">
    <Header />

    <div class="columns">
      <QuestionBox
        class="column is-half is-offset-3"
        v-if="questions.length > 0"
        v-bind:questionData="questions[questionIndex]"
        v-bind:next="handleNext"
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
    }
  },

  methods: {
    handleNext() {
      const finalQuestionIndex = this.questions.length - 1;

      if (this.questionIndex >= 0 && this.questionIndex < finalQuestionIndex) {
        this.questionIndex++;
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
  }
  
}
</script>
