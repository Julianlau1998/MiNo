<template>
  <div>
    <MiniNote
      v-for="note in notes"
      :key="note.id"
      :note="note"
      @open="openNote(note.id)"
      @delete="deleteNote"
    />
    <button @click="add" class="button is-add-button is-bottom-button">
      <i class="fas fa-plus" />
    </button>
  </div>
</template>

<script>
import MiniNote from '@/components/MiniNote.vue'
export default {
  components: {
    MiniNote
  },
  data () {
    return {
      notes: [
      ]
    }
  },
  created () {
    const localNotes = localStorage.getItem('notes')
      if (localNotes) {
        this.notes = JSON.parse(localNotes)
      }
  },
  methods: {
    deleteNote (id) {
      this.notes = this.notes.filter((note) => note.id !== id)
      localStorage.setItem('notes', JSON.stringify(this.notes))
    },
    openNote(id) {
      this.$router.push(`/note/${id}`)
    },
    add () {
      this.$router.push(`/note`)
    }
  }
}
</script>