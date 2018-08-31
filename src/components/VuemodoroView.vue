<template>
    <div>
        <h1>What do you want to work on?</h1>
        <input type="text" v-model="taskName">
        <p>{{taskName}}</p>
    </div>
</template>

<script>


    export default {
        name: 'VumemodoroView',
        data: function () {
            return {
                taskName: ''
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
