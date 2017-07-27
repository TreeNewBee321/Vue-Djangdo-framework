<template>
<div @click="toggle()">
  <span :class="status ? 'highlight' : ''">开</span>
  <span :class="status ? '' : 'highlight'">关</span>
</div>
</template>

<script>
export default {
  props: ['initialStatus'],
  data() {
    return {
      status: false
    }
  },
  methods: {
    toggle() {
      this.status = !this.status
      this.$emit('toggle', this.status)
    }
  },
  created() {
    this.status = this.initialStatus
  }
}
</script>

<style scoped>
span {
  color: red;
  background: #333;
}

span.highlight {
  background: #ccc;
}
</style>
