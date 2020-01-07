<template>
  <div class="block" :class="{ selected: selected }">
    <p> {{value}} </p>
  </div>
</template>

<script>
export default {
  name: 'Block',
  props: {
    type: String,
    value: undefined,
    selected: Boolean
  }
}
</script>

<style scoped>
  .block {
    width: fit-content;
    height: 2em;
    background-color: lightslategrey;
    cursor: pointer;
  }

  .selected {
    background-color: gold;
  }
</style>
