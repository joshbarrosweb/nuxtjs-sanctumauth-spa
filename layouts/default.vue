<template>
  <div class="container w-full max-w-screen">
    <div
      class="flex flex-col max-w-screen-xl p-5 mx-auto md:items-center md:justify-between md:flex-row md:px-6 lg:px-8"
    >
      <div class="flex flex-row items-center justify-between lg:justify-start">
        <a
          href="/"
          class="text-lg font-bold tracking-tighter text-blue-600 transition duration-500 ease-in-out transform tracking-relaxed lg:pr-8"
        >
          Laravel/Nuxt Auth
        </a>
      </div>
      <nav
        class="flex-col items-center flex-grow hidden pb-4 border-blue-600 md:pb-0 md:flex md:justify-end md:flex-row lg:border-l-2 lg:pl-2"
      >
        <NuxtLink
          to="/"
          class="px-4 py-2 mt-2 text-sm text-gray-500 md:mt-0 hover:text-blue-600 focus:outline-none focus:shadow-outline"
          >Home</NuxtLink
        >
        <div class="relative"></div>
        <div
          v-if="!auth"
          class="inline-flex items-center gap-2 list-none lg:ml-auto"
        >
          <NuxtLink to="/auth/login">
            <button
              class="items-center block px-6 py-2.5 text-base font-medium text-center text-blue-600 transition duration-500 ease-in-out transform border-2 border-white shadow-md rounded-xl focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-500"
            >
              Login
            </button>
          </NuxtLink>

          <NuxtLink to="/auth/register">
            <button
              class="items-center block px-6 py-3 text-base font-medium text-center text-white transition duration-500 ease-in-out transform bg-blue-600 rounded-xl hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
            >
              Register
            </button>
          </NuxtLink>
        </div>

        <div
          v-if="auth"
          class="inline-flex items-center gap-2 list-none lg:ml-auto"
        >
          <a href="#" @click="logout">
            <button
              class="items-center block px-6 py-3 text-base font-medium text-center text-white transition duration-500 ease-in-out transform bg-blue-600 rounded-xl hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
            >
              Logout
            </button>
          </a>
        </div>
      </nav>
    </div>

    <Nuxt />
  </div>
</template>

<script>
export default {
  name: 'Layout',

  data() {
    return {
      auth: false,
    }
  },

  mounted() {
    this.$nuxt.$on('auth', (auth) => {
      console.log(auth)

      this.auth = auth
    })
  },

  methods: {
    async logout() {
      await fetch('http://localhost/api/logout', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        credentials: 'include',
      })

      await this.$router.push('/auth/login')
    },
  },
}
</script>
