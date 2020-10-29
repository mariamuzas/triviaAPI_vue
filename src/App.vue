<template>
  <main lang="html">
      <body>
        <h1>Trivia Game</h1>
        <div class="question_details_container">
          <question-details :cards_all="cards"></question-details>
        </div>
        <div class="next_easy">
          <question-filter class="filter" :cards="cards"></question-filter>
          <button @click="click" class="next">Next Question</button>
        </div>
      </body>
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
    fetch('https://opentdb.com/api.php?amount=100')
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
main{
  background-color: #f6eedf;
  height: 100vh;
  width: 100vw;
}
h1 {
  display: flex;
  justify-content: center;
  font-size: 5em;
  color: #ffc115;
  /* background: linear-gradient( 90deg, rgba(255,0,0,1) 15%, rgba(0,0,255,1) 35%, rgba(0,176,0,1 ) 70%, rgb(255, 230, 0) 85%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent; */
  margin: 40px 0;
}
.next_easy{
  display: flex;
  margin: 10px 30px;
  /* justify-content: space; */
}

.next {
  margin: 40px 0 0 50% ;
  padding: 12px;
  background-color: #d63447;
  border: #a72635 solid 1px;
  color: #f6eedf;
  border-radius: 5px;
  text-align: center;
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2), 0 6px 20px 0 rgba(0,0,0,0.19);
  outline: none;
}

.next:hover {
  background-color: #a72635;
}

.filter {
  margin: 0 0 0 20%;
  font-size: 16px;
}

</style>