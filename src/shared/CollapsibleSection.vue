<template>
  <div>
    <div class="header">
      <span v-if="open" @click="open = !open">&#x25b2; Collapse</span>
      <span v-if="!open" @click="open = !open">&#x25bc; Expand</span>
    </div>
    <slot v-if="open">

    </slot>
  </div>
</template>

<script>
export default {
  name: 'CollapsibleSection',
  data() {
    return { open: true };
  },
};
</script>

<style scoped>
  .header {
    background-color: #bbb;
    padding: 3px;
    cursor: pointer;
  }
</style>
