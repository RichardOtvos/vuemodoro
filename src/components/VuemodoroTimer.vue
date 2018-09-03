<template>
    <div>
        <countdown
            class="timer"
            v-bind:time="pomodoroLength"
            v-on:countdownprogress="onCountdownProgress"
            v-on:countdownstart="onCountdownStart"
            v-on:countdownpause="onCountdownPause"
            v-bind:auto-start="false"
            ref="countdown"
        >
            <template slot-scope="props">{{props.minutes}}:{{props.seconds}}</template>
        </countdown>
        <button class="button" v-if="!isCountdownRunning" v-on:click="onStartCountdown">Start</button>
        <button class="button" v-else v-on:click="onPauseCountdown">Pause</button>
        <button class="button" v-on:click="onStopCountdown">Stop</button>
    </div>
</template>

<script>
    import VueCountdown from '@xkeshi/vue-countdown';

    const components = {};
    components[VueCountdown.name] = VueCountdown;

    export default {
        name: 'VuemodoroTimer',
        components,
        props: ['pomodoroMinutes'],
        data: function () {
            return {
                isCountdownRunning: false,
                shouldResetTimer: false,
                pomodoroLength: 0
            }
        },
        created: function () {
            this.pomodoroLength = this.getPomodoroLength();
        },
        methods: {
            //Countdown component emitted events
            onCountdownProgress: function (data) {
                document.title = `${data.minutes}:${data.seconds}`;
            },
            onCountdownStart: function () {
                this.isCountdownRunning = true;
            },
            onCountdownPause: function () {
                this.isCountdownRunning = false;
            },

            //Own events
            onStartCountdown: function () {
                this.$refs.countdown.start();
            },
            onPauseCountdown: function () {
                this.$refs.countdown.pause();
            },
            onStopCountdown: function () {
                this.$refs.countdown.stop();
                this.$refs.countdown.init();
                this.isCountdownRunning = false;
            },
            getPomodoroLength: function () {
                return this.pomodoroMinutes * 60 * 1000;
            }

        }
    }
</script>

<style scoped>
    .timer {
        font-size: 10em;
    }
</style>
