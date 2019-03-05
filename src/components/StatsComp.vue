<template>
    <div class="caption font-weight-thin">
        {{quota}}
    </div>
</template>

<script>
    export default {
        name: "StatsComp",
        props: ['given', 'correct'],
        computed: {
            quota: function() {
                return `${this.correct}/${this.given}`;
            }
        }
    }
</script>

<style scoped>

</style>