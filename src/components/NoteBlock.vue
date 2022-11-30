<template>
    <div class="note-block">
        <textarea 
            class="note-block__area" 
            v-model="text"
            @input="inputText"
            ></textarea>
        <button class="btn btn-save"
            @click="saveNote"
            :disabled="isDisabled"
        >Save Note</button>
    </div>
</template>

<script>
    export default {
        name: 'NoteBlock',
        data() {
            return {
                text: '',
                isDisabled: true,
            }
        },
        methods: {
            saveNote() {
                const note = {
                    id: Date.now(),
                    text: this.text
                }
                this.text = ''
                this.$emit('newNote', note)
            },
            inputText() {
                if (this.text.length > 0) {
                    this.isDisabled = false
                } else {
                    this.isDisabled = true
                }
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