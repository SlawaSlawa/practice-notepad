<template>
    <p>
        {{ msg }}
    </p>
</template>

<script>
    export default {
        name: 'EmptyListMsg',
        data() {
            return {
                msg: 'На данный момент записи отсутствуют...'
            }
        }
    }
</script>