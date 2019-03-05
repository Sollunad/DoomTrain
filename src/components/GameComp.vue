<template>
    <div>
        <StatsComp
            v-bind:given="givenAnswers"
            v-bind:correct="correctAnswers"
            ref="stats"
        ></StatsComp>
        <QuestionComp
                v-on:answer="answer"
                ref="question"
        ></QuestionComp>
        <v-btn
            v-if="answered"
            @click="newQuestion"
        >
            Next
        </v-btn>
    </div>
</template>

<script>
    import QuestionComp from "./QuestionComp";
    import StatsComp from "./StatsComp";
    export default {
        name: "GameComponent",
        components: {StatsComp, QuestionComp},
        data: () => ({
            givenAnswers: 0,
            correctAnswers: 0,
            answered: false,
        }),
        methods: {
            answer: function(correct) {
                this.$refs.stats.giveAnswer(correct);
                this.answered = true;
            },
            newQuestion: function() {
                this.$refs.question.newQuestion();
            }
        }
    }
</script>

<style scoped>

</style>