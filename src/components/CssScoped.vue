<style scoped>
.TextColor{
    color: red;
}
</style>

<template>
    <div class="TextColor">
        <h1>{{msg}}</h1>
    </div>
</template>

<script>
export default {
    data () {
        return {
            msg: 'CSS Scoped!'
        }
    }
}
</script>