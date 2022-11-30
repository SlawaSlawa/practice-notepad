<template>
    <ul class="notes-list">
        <li class="notes-list__item" 
            v-for="note in notes" 
            :key="note.id"
            @click="showNote(note)"    
        >
            {{ note.text }}
            <button 
                class="btn delete-btn"
                title="Удалить запись"
            >X</button>
        </li>
    </ul>
</template>

<script>
    export default {
        name: 'NotesList',
        props: {
            notes: {
                type: Array
            }
        },
        methods: {
            showNote(note) {
                this.$emit('showNote', note)
            }
        }
    }
</script>

<style>
    .notes-list {
        font-size: 12px;
        list-style: none;
    }
    .notes-list__item {
        position: relative;
        border: 1px solid #ccc;
        display: block;
        margin-bottom: 20px;
        padding: 5px;
        height: 60px;
        overflow: hidden;
        cursor: pointer;
        transition: background-color .3s ease;
    }
    .notes-list__item:hover {
        background-color: #ccc;
    }

    .notes-list__item:hover .delete-btn {
        display: flex;
        transition: background-color .3s ease, color .3s ease;
    }

    .notes-list__item:hover .delete-btn:hover {
        background-color: red;
        color: #fff;
    }
</style>