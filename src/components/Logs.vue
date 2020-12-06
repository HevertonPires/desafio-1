<template>
  <ul
    v-if="logs.length"
    style="padding: 0"
  >
    <li
      v-for="(log, idx) in reverseLogs"
      :key="idx"
      class="painel bg-grey h-50"
      v-html="log"
    ></li>
  </ul>
</template>

<script>
export default {
  props: {
    logs: {
      type: Array,
      default: () => [],
    },
  },

  computed: {
    reverseLogs () {
      return [...this.logs].reverse()
    }
  },
}
</script>
