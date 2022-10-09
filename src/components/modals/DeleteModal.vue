<template>
  <div class="is-delete-modal">
      <h3 class="is-size-5 mt-6">
        Are You Sure You want to delete this note?
      </h3>
      <div class="mt-1">
        <button @click="cancel" class="button">
            Cancel
        </button>
        <button @click="deleteDevice" class="button is-danger">
            Delete
        </button>
      </div>
  </div>
</template>

<script>
export default {
    props: {
        note: {
            type: Object,
            default: () => {},
            required: true
        }
    },
    data () {
        return {
            title: ''
        }
    },
    methods: {
        deleteDevice () {
            this.$emit('delete', this.note.id)
        },
        cancel () {
            this.$emit('cancel')
        }
    }
}
</script>