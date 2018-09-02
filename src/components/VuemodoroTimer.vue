<template>
    <div>
        <countdown
            class="timer"
            v-bind:time="getPomodoroLength"
            v-on:countdownprogress="onCountdownProgress"
            v-bind:auto-start="false"
            ref="countdown"
        >
            <template slot-scope="props">{{props.minutes}}:{{props.seconds}}</template>
        </countdown>
        <button class="start-button" v-on:click="onStartCountdown">Start</button>
        <button class="start-button" v-on:click="onPauseCountdown">Pause</button>
        <button class="start-button" v-on:click="onStopCountdown">Stop</button>
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
        computed: {
            getPomodoroLength: function () {
                return this.pomodoroMinutes * 60 * 1000;
            }
        },
        methods: {
            onCountdownProgress: function(data){
              document.title =`${data.minutes}:${data.seconds}`;
            },
            onStartCountdown: function(){
                this.$refs.countdown.start();
            },
            onStopCountdown: function(){
                this.$refs.countdown.stop();
            },
            onPauseCountdown: function(){
                this.$refs.countdown.pause();
            }
        }
    }
</script>

<style scoped>
    .timer{
        font-size: 10em;
    }
</style>
