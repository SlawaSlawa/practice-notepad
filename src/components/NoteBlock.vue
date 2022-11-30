<template>
    <div class="note-block">
        <textarea class="note-block__area" v-model="text"></textarea>
        <button class="btn btn-save"
            @click="saveNote"
        >Save Note</button>
    </div>
</template>

<script>
    export default {
        name: 'NoteBlock',
        data() {
            return {
                text: ''
            }
        },
        methods: {
            saveNote() {
                console.log(this.text);
            }
        }
    }
</script>

<style>
    .note-block {
        height: 100%;
    }
    .note-block__area {
        font-size: 18px;
        padding: 20px;
        width: 100%;
        height: 200px;
    }
    .btn-save {
        display: block;
        margin-left: auto;
    }
</style>