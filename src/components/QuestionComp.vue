<template>
    <div>
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
            picked: null
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
                    const correct = this.correctDay === day;
                    this.$emit('answer', correct);
                }
            },
            newQuestion: function() {
                this.picked = null;
                this.date = this.randomDate();
            }
        },
        created: function () {
            this.newQuestion();
        }
    }
</script>

<style scoped>

</style>