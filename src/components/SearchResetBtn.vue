<template>
    <button 
        class="btn btn--search-reset"
        @click="resetSearchNotes"    
    >Вернуться к списку записей</button>
</template>

<script>
    export default {
        name: 'SearchResetBtn',
        data() {
            return {
            }
        },
        methods: {
            resetSearchNotes() {
                this.$emit('resetSearchNotes')
            }
        }
    }
</script>

<style>
    .btn--search-reset {
        margin-bottom: 20px;
    }
</style>