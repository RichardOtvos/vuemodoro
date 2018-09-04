<template>
    <div class="vuemodoro-timer">
        <countdown
            class="countdown"
            v-bind:time="pomodoroLength"
            v-on:countdownprogress="onCountdownProgress"
            v-on:countdownstart="onCountdownStart"
            v-on:countdownpause="onCountdownPause"
            v-bind:auto-start="false"
            ref="countdown"
        >
            <template slot-scope="props">{{props.minutes}}:{{props.seconds}}</template>
        </countdown>
        <div class="timer-controls">
            <font-awesome-icon class='icon' size="4x" fixed-width icon="play" v-if="!isCountdownRunning" v-on:click="onStartCountdown"/>
            <font-awesome-icon class='icon' size="4x" fixed-width icon="pause" v-else v-on:click="onPauseCountdown"/>
            <font-awesome-icon class='icon' size="4x" fixed-width icon="stop" v-on:click="onStopCountdown"/>
        </div>
    </div>
</template>

<script>
    import VueCountdown from '@xkeshi/vue-countdown';
    import {library} from '@fortawesome/fontawesome-svg-core';
    import {FontAwesomeIcon} from '@fortawesome/vue-fontawesome';
    import {faPlay, faPause, faStop} from '@fortawesome/free-solid-svg-icons';

    library.add(faPlay, faPause, faStop);

    const components = {
        FontAwesomeIcon
    };
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
            this.changePageTitle('Start your Pomodoro!');
        },
        methods: {
            //Countdown component emitted events
            onCountdownProgress: function (data) {
                this.changePageTitle(`${data.minutes}:${data.seconds}`);
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
                this.changePageTitle('Start your Pomodoro!');
            },
            getPomodoroLength: function () {
                return this.pomodoroMinutes * 60 * 1000;
            },
            changePageTitle: function (newTitle) {
                document.title = newTitle;
            }

        }
    }
</script>

<style scoped>
    .countdown {
        font-size: 10em;
    }
    .timer-controls{
        display: inline-flex;
        flex-direction: column;
        position: relative;
        top: -60px;
    }
    .icon{
        color: #e9afb1;
        margin: 5px;
    }

    .icon:hover{
        cursor: pointer;
        color: #be1f2e;
    }
</style>
