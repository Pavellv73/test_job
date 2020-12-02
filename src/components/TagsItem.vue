<template lang="pug">
a(href="#" alt="title") {{title}}
</template>

<script>
export default {
  name:"TagsItem",
  props: {
    title: String,
    id: Number
  }
}
</script>