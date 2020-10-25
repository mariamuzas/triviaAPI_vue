<template>
    <form v-on:submit.prevent="pickDifficulty">
        
        <p>This is my questions filter</p>
        <input type="radio" id="easy" @click="pickDifficulty">
        <label for="easy">Easy</label>
        <hr>
    </form>
</template>

<script>
import { eventBus } from '../main.js'

export default {
    name: "question-filter",
    props:['cards'],

    data(){
        return {
            selectedDifficulty: []
        }
    },

    methods: {
        pickDifficulty: function() {
            let results = this.cards.filter(card => {
                return card.difficulty == "easy"
            })
            this.selectedDifficulty = results

            eventBus.$emit('difficulty-selected', this.selectedDifficulty)
        }
    }
} 
</script>

<style>

</style>