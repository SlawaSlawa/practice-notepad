<template>
    <ul class="notes-list">
        <li class="notes-list__item" 
            v-for="note in notes" 
            :key="note.id">
                {{ note.text }}
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
        }
    }
</script>

<style>
    .notes-list {
        font-size: 12px;
        list-style: none;
    }
    .notes-list__item {
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
</style>