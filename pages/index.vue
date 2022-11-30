<template>
  <div class="d-flex">
    <div class="d-flex w-100 g4" style="padding-right: 50px;">
      <span>{{ location }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomePage',
  layout: 'Navbar',
  data () {
    return {
      location: null
    }
  },
  mounted () {
    this.location = this.$route.name
  }
}
</script>
