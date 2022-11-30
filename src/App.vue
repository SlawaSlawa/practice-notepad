<template>
  <div class="notepad">
    <Title />
    <div class="container">
      <aside class="notes-list-block">
        <NotesList 
          :notes="notesList"
          @showNote="handleShowNote"  
        />
      </aside>
      <main class="main">
        <NoteBlock 
          @newNote="handleNewNote"
          @changeNote="handleChangeNote"
          :note="note"
          ref="noteblock"  
        />
      </main>
    </div>
  </div>
</template>

<script>
import Title from '@/components/Title.vue'
import NotesList from '@/components/NotesList.vue'
import NoteBlock from '@/components/NoteBlock.vue'

export default {
  name: 'App',
  components: {
    Title, NotesList, NoteBlock,
  },
  emits: ['newNote', 'showNote', 'changeNote'],
  data() {
    return {
      notesList: [
        {
          id: 1,
          text: 'Lorem'
        },
        {
          id: 2,
          text: 'Tfsajfsadfklsd'
        },
        {
          id: 3,
          text: 'LKHJKHhkjhkjhjkhjkh jkhkjhjk LKHJKHhkjhkjhjkhjkh jkhkjhjkLKHJKHhkjhkjhjkhjkh jkhkjhjkLKHJKHhkjhkjhjkhjkh jkhkjhjkLKHJKHhkjhkjhjkhjkh jkhkjhjkLKHJKHhkjhkjhjkhjkh jkhkjhjkLKHJKHhkjhkjhjkhjkh jkhkjhjkLKHJKHhkjhkjhjkhjkh jkhkjhjkLKHJKHhkjhkjhjkhjkh jkhkjhjkLKHJKHhkjhkjhjkhjkh jkhkjhjkLKHJKHhkjhkjhjkhjkh jkhkjhjkLKHJKHhkjhkjhjkhjkh jkhkjhjkLKHJKHhkjhkjhjkhjkh jkhkjhjkLKHJKHhkjhkjhjkhjkh jkhkjhjk'
        },
      ],
      note: {},
    }
  },
  methods: {
    handleNewNote(note) {
      this.notesList.unshift(note)
    },
    handleShowNote(note) {
      this.$refs.noteblock.showNote(note)
    },
    handleChangeNote(changeText, id) {
      this.notesList = this.notesList.map(note => {
        if(note.id === id) {
          return {
            id: id,
            text: changeText,
          }
        } else {
          return note
        }
      })
    }
  }
}
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

.btn {
  cursor: pointer;
}

.container {
  max-width: 1024px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: start;
  gap: 20px;
}

.notes-list-block {
  border: 1px solid #2c3e50;
  border-radius: 5px;
  padding: 20px;
  overflow-y: auto;
  width: 20%;
  max-height: 50vh;
}

.notepad {
  height: 100vh;
}

.main {
  width: 100%;
  height: 100%;
}
</style>
