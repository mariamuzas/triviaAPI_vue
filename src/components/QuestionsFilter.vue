<template>
    <form v-on:submit.prevent>
        <input type="radio" id="easy" @click="pickEasy">
        <label for="easy">Easy mode</label>
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
        pickEasy: function() {
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