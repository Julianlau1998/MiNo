<template>
  <div class="notes">
    <MiniNote
      v-for="note in notes"
      :key="note.id"
      :note="note"
      @open="openNote(note.id)"
      @delete="openDeleteModal(note)"
    />
    <button @click="add" class="button is-add-button is-bottom-button">
      <i class="fas fa-plus" />
    </button>
    <DeleteModal
        v-if="showDeleteModal"
        :note="noteToDelete"
        @delete="deleteNote"
        @cancel="hideDeleteModal"
    />
  </div>
</template>

<script>
import MiniNote from '@/components/MiniNote.vue'
import DeleteModal from '@/components/modals/DeleteModal.vue'
export default {
  components: {
    MiniNote,
    DeleteModal
  },
  data () {
    return {
      notes: [
      ],
      showDeleteModal: false,
      noteToDelete: {}
    }
  },
  created () {
    const localNotes = localStorage.getItem('notes')
      if (localNotes) {
        this.notes = JSON.parse(localNotes)
      }
  },
  methods: {
    openDeleteModal (note) {
      this.showDeleteModal = true
      this.noteToDelete = note
    },
    hideDeleteModal () {
      this.showDeleteModal = false
      this.deviceToDelete = {}
    },
    deleteNote (id) {
      this.notes = this.notes.filter((note) => note.id !== id)
      localStorage.setItem('notes', JSON.stringify(this.notes))
      this.showDeleteModal = false
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