<template>
    <div id="app">
        <VuemodoroView/>
        <VuemodoroTimer v-bind:pomodoro-minutes="25"/>
    </div>
</template>

<script>
    import VuemodoroView from './components/VuemodoroView.vue'
    import VuemodoroTimer from './components/VuemodoroTimer.vue';
    export default {
        name: 'app',
        components: {
            VuemodoroView,
            VuemodoroTimer
        }
    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
