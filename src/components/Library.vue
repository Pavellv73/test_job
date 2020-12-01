<template lang="pug">
section.books
  Book.books__item(
    v-for="item in items"
    :title="item.name"
  )
</template>

<script>
import Book from "./Book"
export default {
  name: "library",
  props: {
    items: Array
  },
  components: {
    Book
  },
}
</script>

<style lang="scss">
  .books {
    width: 100%;
    display: flex;
    flex-wrap: wrap;

    &__item {
      display: block;
      width: 32%;
      margin-right: 10px;
      margin-bottom: 10px;
    }
  }
</style>