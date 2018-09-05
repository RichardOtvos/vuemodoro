<template>
    <div class="vuemodoro-timer">
        <countdown
            class="countdown"
            v-bind:time="pomodoroLength"
            v-on:countdownprogress="onCountdownProgress"
            v-on:countdownstart="onCountdownStart"
            v-on:countdownpause="onCountdownPause"
            v-on:countdownend="onCountdownEnd"
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
        props: ['pomodoroMinutes','pomodoroEndSound', 'breakMinutes', 'breakEndSound'],
        data: function () {
            return {
                isCountdownRunning: false,
                shouldResetTimer: false,
                pomodoroLength: 0,
                breakLength: 0
            }
        },
        created: function () {
            this.pomodoroLength = this.getMinutesInMs(this.pomodoroMinutes);
            this.breakLength = this.getMinutesInMs(this.breakMinutes);
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
            onCountdownEnd: function () {
                this.isCountdownRunning = false;
                this.playSound(this.pomodoroEndSound);
                this.changePageTitle('Start your Pomodoro!');

            },

            //Own events
            onStartCountdown: function () {
                this.$refs.countdown.start();
            },
            onPauseCountdown: function () {
                this.$refs.countdown.pause();
            },
            onStopCountdown: function () {
                this.$refs.countdown.pause();
                this.$refs.countdown.init();
                this.changePageTitle('Start your Pomodoro!');
            },

            //Non-event methods
            getMinutesInMs: function (timeInMinutes) {
                return timeInMinutes * 60 * 1000;
            },
            changePageTitle: function (newTitle) {
                document.title = newTitle;
            },
            playSound (sfxName) {
                if(sfxName) {
                    const audio = new Audio(`/sounds/${sfxName}.mp3`);
                    audio.play();
                }
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
