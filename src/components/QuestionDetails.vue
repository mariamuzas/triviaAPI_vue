<template lang="html">
  <article>
        <div class="details">
            <div class="category">
                <p class="detail">Category</p>
                <p class="card_details">{{currentQuestion.category}}</p>
            </div>
            <div class="difficulty">
                <p class="detail">Difficulty</p>
                <p class="card_details">{{currentQuestion.difficulty}}</p>
            </div>
        </div>
            <div class="question">
                <h2>{{currentQuestion.question}}</h2>
                <ul>
                    <li v-for="(pos, index) in answers" :key="index">{{pos}}</li>
                </ul>
            </div>
            <div class="answer">
                <button class="check_answer" v-on:click="handlingClick">Check your answer</button>
                <p>{{answer}}</p>
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
    margin: 30px 5% 0 5%;
}

.details {
    display: flex; 
    margin-left: 7%;
}

.category, .difficulty {
    display: flex;
    padding: 4px;
    margin: 10px 30px;
}

.difficulty {
    margin-left: 60%;
    position: absolute;
}
.detail, .card_details {
    padding: 8px;
    margin: 0px;
    font-size: 15px;
    font-weight: 550;
    /* border: solid 1px; */
}
.detail {
    background-color: #d63447;
    color: #f6eedf;
    border-radius: 5px 0 0 5px;
    text-align: center;
}
.card_details {
    border: solid #d63447 1px;
    border-radius: 0 5px 5px 0;
    text-align: center;
}

.question {
    position: absolute;
    /* font-size: 30px; */
    margin: 40px 15%;
}
.answer { 
    display: flex;
    justify-content: space-between;
    /* border: solid 1px; */
    padding: 10px;
    margin: 260px 30% 20px 18%;
    border: solid #ffd31d;
}

.question > ul {
    margin: 15px 80px;
    font-size: 18px;
}

.check_answer {
    /* position: absolute; */
    background-color:#f57b51;
    box-shadow: 0 2px 10px 0 rgba(0,0,0,0.2), 0 2px 10px 0 rgba(0,0,0,0.19);
    color: #f6eedf;
    font-weight: 600;
    border: #e6663f solid 1px;
    border-radius: 5px;
    padding: 10px;
    outline:none;
}
 .check_answer:hover {
     background-color: #ffbb29;
     color: #f6eedf;
 }

 .answer > p {
     font-size: 18px;
     position:absolute;
     margin-left: 200px;
     margin-top: 5px;
 }

</style>