<template>
    <div class="note-block">
        <textarea 
            class="note-block__area" 
            v-model="text"
            @input="inputText"
            ></textarea>

        <div class="note-block__btns-wrap">
            <button class="btn btn-clear"
                @click="clearNote"
            >Clear Note</button>
            <button class="btn btn-save"
                @click="saveNote"
                :disabled="isDisabled"
            >
                Save Note
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'NoteBlock',
        props: {
            note: {
                type: Object,
            }
        },
        data() {
            return {
                id: null,
                text: '',
                isDisabled: true,
            }
        },
        methods: {
            saveNote() {
                if (this.id) {
                    this.$emit('changeNote', this.text, this.id)
                    this.id = null
                } else {
                    const note = {
                        id: Date.now(),
                        text: this.text
                    }
                    this.text = ''
                    this.$emit('newNote', note)
                }
                this.text = ''
                this.id = null
            },
            inputText() {
                if (this.text.trim().length > 0) {
                    this.isDisabled = false
                } else {
                    this.isDisabled = true
                }
            },
            showNote(note) {
                this.text = note.text
                this.isDisabled = false
                this.id = note.id
            },
            clearNote() {
                this.text = ''
                this.inputText()
            },
        }
    }
</script>

<style>
    .note-block {
        height: 100%;
    }
    .note-block__area {
        font-size: 18px;
        margin-bottom: 20px;
        padding: 20px;
        width: 100%;
        height: 200px;
    }
    .note-block__btns-wrap {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
</style>