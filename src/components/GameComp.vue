<template>
    <div>
        <StatsComp
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
            answered: true,
        }),
        methods: {
            answer: function(isCorrect) {
                this.$refs.stats.giveAnswer(isCorrect);
                this.answered = true;
            },
            newQuestion: function() {
                this.$refs.question.newQuestion();
                this.answered = false;
            }
        }
    }
</script>

<style scoped>

</style>