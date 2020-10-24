  computed: {
        answers() {
            // this.posible_answers = this.currentQuestion.incorrect_answers.concat(this.currentQuestion.correct_answer)
            let answers = [...this.currentQuestion.incorrect_answers]
            answers.push(this.currentQuestion.correct_answer)
            shuffle(answers)

            return answers

            // const answer_choices = [...this.currentQuestion.incorrect_answers]
            // question_answer = Math.floor(Math.random() * 3) +1
            // answer_choices.splice(question_answer -1, 0, this.currentQuestion.correct_answer)

            // this.posible_answers = answer_choices
        }

    },