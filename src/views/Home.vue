<template>
  <div class="home">
    <topNav />
    <notes />
  </div>
</template>

<script>
import notes from '@/components/Notes.vue'
import topNav from '@/components/TopNav.vue'

export default {
  name: 'Home',
  components: {
    notes,
    topNav
  }
}
</script>
