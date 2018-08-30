<template>
    <div>
        <h1>What task are you working on?</h1>
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
