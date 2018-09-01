<template>
    <div>
        <countdown v-bind:time="getPomodoroLength" class="timer">
            <template slot-scope="props">{{props.minutes}}:{{props.seconds}}</template>
        </countdown>
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
        data: function () {
            return {}
        }
    }
</script>

<style scoped>
    .timer{
        font-size: 10em;
    }
</style>
