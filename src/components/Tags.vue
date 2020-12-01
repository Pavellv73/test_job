<template lang="pug">
div.tags
  div.tags__wrapper
    TagsItem.tags__item(v-for="item in tags" :title="item.name")
</template>

<script>
import TagsItem from './TagsItem'

export default {
  name: 'Tags',
  props: {
    tags: Array
  },
  components: {
    TagsItem
  },
}
</script>

<style lang="scss">
  .tags {
    width: 100%;

    &__wrapper {
      width: 100%;
      display: flex;
    }

    &__item {
      font: 300 16px/18px Arial, sans-serif;
      padding: 5px 10px;
      margin-right: 10px;
      text-decoration: none;
      border-radius: 100px;
      background-color: gainsboro;
      color: white;
      transition: background-color 0.3s ease;

      &:hover {
        background-color: hotpink;
      }

      &:last-child {
        margin-right: 0;
      }

      &--active {
        background-color: deeppink;
      }
    }
  }
</style>
