<template>
    <div id="app">
        <VuemodoroTimer
            v-bind:pomodoro-minutes="25"
            pomodoro-end-sound="bell"
            v-bind:break-minutes="5"
            break-end-sound="bell"
        />
        <img src="./assets/pomo.svg" alt="" aria-hidden="true">
    </div>
</template>

<script>
    import VuemodoroView from './components/VuemodoroView.vue';
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
        box-sizing: border-box;
        text-align: center;
        color: #2c3e50;
        padding-top: 60px;
        display: flex;
        flex-direction: column;
        height: 100vh;
    }

    #app img{
        padding-bottom: 30px;
    }
</style>
