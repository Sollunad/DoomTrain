<template>
    <div class="caption font-weight-light">
        {{quota}}
        Streak: {{streak}}
    </div>
</template>

<script>
    export default {
        name: "StatsComp",
        data: () => ({
            given: 0,
            correct: 0,
            streak: 0,
        }),
        computed: {
            quota: function() {
                return `${this.correct}/${this.given}`;
            }
        },
        methods: {
            giveAnswer: function(isCorrect) {
                this.given++;
                if (isCorrect) {
                    this.correct++;
                    this.streak++;
                } else {
                    this.streak = 0;
                }
            }
        }
    }
</script>

<style scoped>

</style>