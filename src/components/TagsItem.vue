<template lang="pug">
span(
  :class="{'.tags__item--active': isActive}"
  @click="this.$emit('getId', id)") {{title}}
</template>

<script>
export default {
  name:"TagsItem",
  props: {
    title: String,
    id: Number,
    isActive: Boolean
  }
}
</script>