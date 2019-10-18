<template>
  <div class="mt-2 p-4 bg-gray-800 text-white rounded">
    <div class="flex ">
      <div class="text-lg font-semibold">{{ charge.name }}</div>
      <div class="ml-2">
        <span v-if="charge.punishment.jail" class="bg-red-700 px-2 py-1 text-xs font-semibold tracking-tight uppercase rounded-full">
          {{ charge.punishment.jail }} <span class="text-xs">years</span>
        </span>
        <span v-if="charge.punishment.jail && charge.punishment.fine" class="uppercase px-1 text-xs font-semibold text-gray-500">or</span>
        <span v-if="charge.punishment.fine" class="bg-gray-700 px-2 py-1 text-xs font-semibold tracking-tight uppercase rounded-full">
          {{ charge.punishment.fine | currency }}
        </span>
        <span v-if="charge.punishment.special" class="bg-gray-700 px-2 py-1 text-xs font-semibold tracking-tight uppercase rounded-full">
          {{ charge.punishment.special }}
        </span>
      </div>
    </div>
    <p class="text-gray-500 truncate">
      {{ charge.description }}
    </p>
  </div>
</template>
<script>
export default {
  props: ['charge'],
}
</script>
