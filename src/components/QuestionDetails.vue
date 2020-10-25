<template>
  <article>
        <div class="details">
            <p>Category:{{currentQuestion.category}}</p>
            <p>Difficulty: {{currentQuestion.difficulty}}</p>
        </div>
        <h2>{{currentQuestion.question}}</h2>
        <ul>
            <li v-for="(pos, index) in answers" :key="index">{{pos}}</li>
        </ul>
        <div class="answer">
            <button v-on:click="handlingClick">Check your answer</button>
            <p>{{answer}}.</p>
        </div>
  </article>
</template>

<script>
import {eventBus} from '@/main.js';

export default {
    name: "question-details",
    props:['cards_all'],

    data() {
        return {
        curr: 0,
        currentQuestion: {
            "category": "Entertainment: Video Games",
            "type": "boolean",
            "difficulty": "medium",
            "question": "Amazon acquired Twitch in August 2014 for $970 million dollars.",
            "correct_answer": "True",
            "incorrect_answers": [
            "False"
            ]},

        answer: null,

        answerIndexRandom: null,
        }
    },

    methods: {
        nextQuestion: function() {
        this.currentQuestion = this.cards_all[this.curr++]
        this.answer = null
            },
    
        handlingClick: function() {
            this.answer = this.currentQuestion.correct_answer
            }
        },
        
    created: function() {
    this.$parent.$on('update', this.nextQuestion);
    },

    computed: {
        answers() {
            let answers = [...this.currentQuestion.incorrect_answers];
            this.answerIndexRandom = Math.floor(Math.random() * 3) + 1;
            answers.splice(this.answerIndexRandom -1, 0, this.currentQuestion.correct_answer);

            return answers
        }
    },
}
</script>

<style scoped>
article{
    margin: 100px;
}

.details {
    display: flex; 
    justify-content: space-between;

}
.answer {
    display: flex;
    justify-content: space-between;
    border: solid 1px;
    padding: 10px;
    margin: 10px 60px;
}

</style>