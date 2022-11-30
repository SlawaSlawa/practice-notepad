<template>
    <h1 class="title">{{ titleText }}</h1>
</template>

<script>
    export default {
        name: 'Title',
        data() {
            return {
                titleText: 'NotePad',
            }
        }
    }
</script>

<style lang="scss">
    .title {
        text-align: center;
        margin-bottom: 20px;
    }
</style>