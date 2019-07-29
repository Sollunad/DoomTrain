<template>
    <div>
        <v-progress-circular size="50" width="5" :value="timeRatio" :color="timerColor" class="timer">
            {{timeRatio / 10}}
        </v-progress-circular>
        <div class="display-2 font-weight-light">
            {{dateString}}
        </div>
        <ButtonsComp
            v-on:pick="pick"
            v-bind:correct="correctDay"
            v-bind:picked="picked"
        ></ButtonsComp>
    </div>
</template>

<script>
    import ButtonsComp from "./ButtonsComp";
    export default {
        name: "QuestionComp",
        components: {ButtonsComp},
        data: () => ({
            date: null,
            picked: null,
            maxTime: 10,
            remainingTime: 0,
            timer: null,
            startedTimestamp: null,
            timerColor: ''
        }),
        computed: {
            dateString: function() {
                let d = this.date.getDate();
                d = d > 9? d : `0${d}`;
                let m = this.date.getMonth() + 1;
                m = m > 9? m : `0${m}`;
                const y = this.date.getFullYear();
                return `${d}.${m}.${y}`;
            },
            correctDay: function() {
                return this.date.getDay();
            },
            timeRatio: function() {
                return Math.ceil(this.remainingTime / this.maxTime * 100);
            }
        },
        methods: {
            randomDate: function () {
                const start = new Date(1800, 0, 1);
                const end = new Date(2199, 0, 1);
                return new Date(start.getTime() + Math.random() * (end.getTime() - start.getTime()));
            },
            pick: function(day) {
                if (!this.picked) {
                    this.picked = day;
                    clearInterval(this.timer);
                    const correct = this.correctDay === day;
                    this.$emit('answer', correct);
                }
            },
            newQuestion: function() {
                this.picked = null;
                this.timerColor = '';
                this.remainingTime = this.maxTime;
                this.startedTimestamp = Date.now();
                const that = this;
                this.timer = setInterval(function() {
                    that.remainingTime--;
                    if (that.remainingTime === 0) {
                        that.pick(7);
                        that.timerColor = 'error';
                    }
                }, 1000);
                this.date = this.randomDate();
            }
        },
        created: function () {
            this.newQuestion();
        }
    }
</script>

<style scoped>
    .timer {
        margin: 15px 0;
    }
</style>