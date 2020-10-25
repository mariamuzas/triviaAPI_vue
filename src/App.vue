<template>
  <main>
      <h1>Trivia Questions</h1>
    <div class="question_details_container">
      <question-details :cards_all="cards"></question-details>
    </div>
    <div class="next_easy">
      <question-filter :cards="cards"></question-filter>
      <button @click="click">Next Question</button>
    </div>
  </main>
</template>

<script>
import QuestionFilter from '@/components/QuestionsFilter.vue'
import QuestionDetails from '@/components/QuestionDetails.vue'
import {eventBus} from '@/main.js';

export default {
  name: "app",

  data(){
    return {
      cards: [],
    }
  }, 

  mounted() {
    fetch('https://opentdb.com/api.php?amount=80')
    .then(res => res.json())
    .then(data => this.cards = data.results)

    eventBus.$on('difficulty-selected', (cards_selected) => {
      this.cards = cards_selected
    })
  },

  components: {   
    QuestionFilter, 
    QuestionDetails
  },
  
  methods: {
    click: function() {
        this.$emit('update');
    }
  }
}
</script>

<style scoped>
.next_easy{
  display: flex;
  justify-content: space-evenly;
}

</style>