<template>
  <div class="miniNote">
      <div class="columns is-mobile">
          <div @click="openNote" class="column is-10 is-align-left">
                <h2 class="heading is-size-5">
                    {{ note.note.substring(0, 11) }}
                </h2>
          </div>
          <div @click="deleteNote" class="column is-2">
                <h2 class="heading is-size-5">
                    <i class="fas fa-trash is-secondary is-cursor-default" />
                </h2>
          </div>
      </div>
  </div>
</template>

<script>
export default {
    props: {
        note: {
            type: Object,
            required: true,
            default: () => {}
        }
    },
    methods: {
        deleteNote () {
            this.$emit('delete', this.note.id)
        },
        openNote () {
            this.$emit('open')
        }
    }
}
</script>

<style>

</style>