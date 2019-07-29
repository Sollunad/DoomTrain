<template>
    <div class="caption font-weight-light">
        {{quota}}
        Streak: {{stats.streak}}
    </div>
</template>

<script>
    export default {
        name: "StatsComp",
        data: () => ({
            stats: {
                given: 0,
                correct: 0,
                streak: 0,
            }
        }),
        computed: {
            quota: function() {
                return `${this.stats.correct}/${this.stats.given}`;
            }
        },
        methods: {
            giveAnswer: function(isCorrect) {
                this.stats.given++;
                if (isCorrect) {
                    this.stats.correct++;
                    this.stats.streak++;
                } else {
                    this.stats.streak = 0;
                }
                this.saveStats();
            },
            saveStats: function() {
                const dataString = JSON.stringify(this.stats);
                localStorage.setItem('stats', dataString);
            },
            getStats: function() {
                const dataString = localStorage.getItem('stats');
                if (dataString) this.stats = JSON.parse(dataString);
            }
        },
        created: function() {
            this.getStats();
        }
    }
</script>

<style scoped>

</style>