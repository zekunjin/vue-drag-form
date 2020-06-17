<template>
  <div>
    {{ value }}
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: Object,
      default: () => ({})
    }
  }
}
</script>
