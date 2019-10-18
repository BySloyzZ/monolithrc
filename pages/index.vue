<template>
  <div>
    <Navbar/>
    <div class="container mx-auto p-4">
      <h1 class="font-semibold text-3xl text-white">
        MonolithRP Resource Compilation
      </h1>
      <p class="text-gray-100 text-xl">A collection of various tools, guides and resources related to the Monolith Roleplay Garry's Mod server.</p>
      <section class="pt-4">
        <h2 class="font-bold tracking-tight text-gray-400 uppercase">Law Enforcement</h2>
        <div class="flex pt-2">
          <nuxt-link class="w-full lg:w-1/2 p-6 bg-gray-800 font-semibold font-xl text-white rounded shadow hover:shadow-lg hover:bg-gray-700" to="/police/calculator">
            <span class="text-sm uppercase text-semibold tracking-tighter text-blue-100 bg-blue-800 px-2 rounded-lg">Tool</span>
            Law Enforcement Punishment Lookup
          </nuxt-link>
        </div>
      </section>
    </div>
    <FooterContent/>
  </div>
</template>
<script>
import Navbar from '~/components/Navbar.vue'
import FooterContent from '~/components/FooterContent.vue'

export default {
  components: {
    Navbar,
    FooterContent
  }
}

</script>
<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/

</style>
