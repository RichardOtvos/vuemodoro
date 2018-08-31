<template>
    <div class="timer">
        {{getPomodoroLength}} ms left
    </div>
</template>

<script>
    export default {
        name: 'VuemodoroTimer',
        props: ['pomodoroMinutes'],
        computed:{
            getPomodoroLength: function(){
                return this.pomodoroMinutes * 60 * 1000;
            }
        },
        data: function () {
            return {
            }
        }
    }
</script>

<style scoped>

</style>
