<template>
  <div class="note">
    <topNav />
      <!-- <input
        type="text"
        class="titleInput"
        placeholder="title"
        v-model="note.title"
        @keyup.enter="goToNote"
    />
    <br> -->
    <i @click="save" class="fas fa-check is-save-icon"></i>
    <i @click="back" class="fas fa-arrow-left is-back-icon"></i>
    <textarea
        type="text"
        class="noteInput"
        placeholder="note"
        v-model="note.note"
        ref="note"
    />
    <!-- <button @click="save" class="button is-bottom-button is-save-button">
      Save
    </button> -->
  </div>
</template>

<script>
import { uuid } from 'vue-uuid'
import topNav from '@/components/TopNav.vue'

export default {
    components: { topNav },
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
    mounted () {
      this.$refs.note.focus()
    },
    methods: {
        goToNote () {
            this.$refs.note.focus()
        },
        save () {
            if(!this.note.note.length) {
                this.$refs.note.focus()
                return
            }
            
            !this.edit ? this.create() : this.editNote()
        },
        back () {
          this.$router.push('/')
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
