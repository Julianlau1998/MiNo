<template>
  <div class="note">
      <!-- <input
        type="text"
        class="titleInput"
        placeholder="title"
        v-model="note.title"
        @keyup.enter="goToNote"
    />
    <br> -->
      <textarea
        type="text"
        class="noteInput"
        placeholder="note"
        v-model="note.note"
        ref="note"
    />
    <button @click="save" class="button is-bottom-button is-save-button">
      Save
    </button>
  </div>
</template>

<script>
import { uuid } from 'vue-uuid'

export default {
    data () {
        return {
            note: {
                title: '',
                note: ''
            },
            notes: [],
            edit: false
        }
    },
    created () {
        const id = this.$route.params.id
        let localNotes = localStorage.getItem('notes')
        if (!localNotes) {
            this.notes = []
        } else {
            this.notes = JSON.parse(localNotes)
        }

        if (id?.length) {
            this.edit = true
            this.getNoteById(id)
        }
    },
    methods: {
        goToNote () {
            this.$refs.note.focus()
        },
        save () {
            if(!this.note.note.length) return
            
            !this.edit ? this.create() : this.editNote()
        },
        create () {
            this.note.id = uuid.v4()
            this.notes.push(this.note)
            localStorage.setItem('notes', JSON.stringify(this.notes))
            this.$router.push('/')
        },
        editNote () {
            console.log(this.notes)
            const index = this.notes.findIndex((note => note.id == this.$route.params.id))
            console.log(index)
            this.notes[index] = this.note
            localStorage.setItem('notes', JSON.stringify(this.notes))
            this.$router.push('/')
        },
        getNoteById (id) {
            this.note = this.notes.filter((note) => note.id == id)[0]
        }
    }
}
</script>