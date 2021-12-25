<template>
  <div>
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  name: 'Home',

  data() {
    return {
      message: '',
    }
  },

  async mounted() {
    try {
      const response = await fetch('http://localhost/api/user', {
        headers: { 'Content-Type': 'application/json' },
        credentials: 'include',
      })

      const content = await response.json()

      console.log(content)

      this.message = 'Hello ' + content.name
      this.$nuxt.$emit('auth', true)
    } catch (e) {
      this.message = 'You are not logged in'
      this.$nuxt.$emit('auth', false)
    }
  },
}
</script>
