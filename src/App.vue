<template>
  <main>
    <h1>Trivia Questions</h1>
  </main>
</template>

<script>
export default {
  data(){
    return {
      cards: []
    }
  }, 
  
  mounted() {
    fetch('https://opentdb.com/api.php?amount=40&type=multiple')
    .then(res => res.json())
    .then(cards => this.cards = cards.results)
  }
}
</script>

<style>

</style>