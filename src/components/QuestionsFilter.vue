<template>
    <form>
        <hr>
        <p>This is my questions filter</p>
        <select>
            <option>Select category for your question...</option>
            <option v-for="card in cards" :value="difficulty">{{card.difficulty}}</option>
        </select>
        <hr>
    </form>
</template>

<script>

export default {
    name: "question-filter",
    // data(){

    // },
    props:['cards']
}
</script>

<style>

</style>