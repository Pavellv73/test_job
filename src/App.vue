<template lang="pug">
section.wrapper
  Tags(:tags="list")
</template>

<script>
import Tags from './components/Tags.vue';
import axios from 'axios';

export default {
  name: 'App',
  data() {
    return {
      list: null
    }
  },
  components: {
    Tags
  },
  mounted() {
    axios
        .post('https://webdev.modumlab.com/api/book/categories')
        .then(response => (this.list = response.data.data.list));
  }
}
</script>

<style lang="scss">
  .wrapper {
    width: 70%;
    margin: 0 auto;
    padding: 50px 0 50px;
  }
</style>
