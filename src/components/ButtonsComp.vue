<template>
    <div>
        <v-btn
            v-for="day in weekdayNumbers"
            v-bind:key="day"
            @click="pickDay(day)"
            :color="buttonColor(day)"
        >
            {{weekdayAbbr[day]}}
        </v-btn>
    </div>
</template>

<script>
    export default {
        name: "ButtonsComp",
        props: ['correct', 'picked'],
        data: () => ({
            weekdayNumbers: [0,1,2,3,4,5,6],
            weekdayAbbr: ['So', 'Mo', 'Di', 'Mi', 'Do', 'Fr', 'Sa']
        }),
        methods: {
            pickDay: function(day) {
                this.$emit('pick', day);
            },
            buttonColor: function(day) {
                if (this.isGreen(day)) return 'success';
                else if (this.isRed(day)) return 'error';
                else return '';
            },
            isGreen: function(day) {
                return this.picked && day === this.correct;
            },
            isRed: function(day) {
                return this.picked === day && this.picked !== this.correct;
            },
        }
    }
</script>

<style scoped>

</style>