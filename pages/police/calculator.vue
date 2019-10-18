<template>
  <div>
    <Navbar />
    <div class="container mx-auto p-4">
      <div class="flex items-center">
        <h1 class="font-semibold text-3xl text-white">
          Law Enforcement Punishment Lookup
        </h1>
        <div class="ml-2">
          <span class="inline-block uppercase text-sm font-semibold bg-blue-700 text-white py-1 px-2 rounded-full">Beta</span>
        </div>
      </div>
      <p class="text-gray-100 text-xl">A tool to easily calculate fine or jail time amounts based on the charges.</p>
      <Calculator />
    </div>
    <FooterContent />
  </div>
</template>
<script>
import Navbar from '~/components/Navbar.vue'
import FooterContent from '~/components/FooterContent.vue'
import Calculator from '~/components/calculator/Calculator.vue'

export default {
  components: {
    Navbar,
    FooterContent,
    Calculator,
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
