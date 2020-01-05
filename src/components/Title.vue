<template>
  <div>
    <h1>sound blocks</h1>
    <div id="desc">
    <h4>a drag-and-drop playground for audio synthesis</h4>
    <h4>created by Colin Scruggs</h4>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Title',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1 {
    margin: 0 0.5rem;
  }

  h4 {
    margin: 0.5rem;
    color: #4f5e6d;
  }

  #desc {
    display: flex;
    justify-content: space-between;
  }
</style>
