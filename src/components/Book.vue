<template lang="pug">
div.book
  h3 {{title}}
</template>

<script>
export default {
  name: "Book",
  props: {
    title: String
  }
}
</script>

<style lang="scss">
  .book {
    border-radius: 10px;
    border: 1px solid black;
  }
</style>