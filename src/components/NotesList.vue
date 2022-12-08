<template>
    <EmptyListMsg v-if="(notes.length < 1)"/>
    <div class="notes-list-wrapper" v-else>
        <label class="search">
            Поиск: 
            <input class="search__input" type="text" 
                @input="searchNotes"
                v-model="searchText"    
            >
        </label>

        <SearchResetBtn 
            @resetSearchNotes="handleResetSearchNotes"
            v-show="isSearch"    
        />

        <ul class="notes-list" v-if="!isSearch">
            <li class="notes-list__item" 
                v-for="note in notes" 
                :key="note.id"
                @click="showNote(note)"    
            >
                {{ note.text }}
                <button 
                    class="btn delete-btn"
                    title="Удалить запись"
                    @click.stop="deleteNote(note.id)"
                >X</button>
            </li>
        </ul>

        <div class="search__notes" v-else>
            <h4 v-show="findNotesList.length <= 0">Даных записей не найдено...</h4>
            <ul class="notes-list" >
                <li class="notes-list__item" 
                    v-for="findNote in findNotesList" 
                    :key="findNote.id"
                    @click="showNote(findNote)"    
                >
                    {{ findNote.text }}
                    <button 
                        class="btn delete-btn"
                        title="Удалить запись"
                        @click.stop="deleteNote(findNote.id)"
                    >X</button>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
import EmptyListMsg from '@/components/EmptyListMsg.vue';
import SearchResetBtn from '@/components/SearchResetBtn.vue';

    export default {
    name: "NotesList",
    components: { EmptyListMsg, SearchResetBtn },
    props: {
        notes: {
            type: Array
        },
        changeId: {
            type: Number,
        }
    },
    emits: ['resetSearchNotes'],
    data() {
        return {
            searchText: '',
            isSearch: false,
            findNotesList: [],
        }
    },
    methods: {
        showNote(note) {
            this.$emit("showNote", note);
        },
        deleteNote(id) {
            this.findNotesList  = this.findNotesList.filter(findNote => findNote.id !== id)
            this.$emit("deleteNote", id);
        },
        searchNotes() {
            const searchText = this.searchText.toLowerCase()

            if (searchText.length > 2) {
                this.isSearch = true
                this.findNotesList.length = 0

                this.notes.forEach(note => {
                    if (note.text.toLowerCase().indexOf(searchText) >= 0) {
                            this.findNotesList.push(note)
                    }
                })
                this.findNotesList = Array.from(new Set(this.findNotesList))

                this.findNotesList = this.findNotesList.map(findNote => findNote)

            } else {
                this.isSearch = false
            }
        },
        changeSearchNotes(id, newText) {
            this.findNotesList.forEach(note => {
                if (note.id === id) {
                    note.text = newText
                }
            })
        },
        handleResetSearchNotes() {
            this.findNotesList.length = 0
            this.searchText = ''
            this.isSearch = false
        }
    },
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
        margin-bottom: 10px;
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

    .search {
        display: block;
        margin-bottom: 5px;
    }

    .search__input {
        display: block;
        width: 100%;
    }
</style>