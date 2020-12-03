<template lang="pug">
section.books
  Book.books__item(
    v-for="item in items"
    :title="item.name"
    :author="item.author"
    :description="item.description"
    :year="item.year"
    :image="item.image"
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
  }
}
</script>

<style lang="scss">
.books {
  width: 100%;
  min-height: 360px;
  display: flex;
  flex-wrap: wrap;

  &__item {
    display: block;
    width: calc(100% / 3);
    margin-bottom: 10px;

    &:nth-child(3n) {
      margin-right: 0;
    }
  }
}
</style>