<template lang="pug">
section.wrapper
  Tags.wrapper__categories(:tags="categories" v-model="updateBooks")
  Library.wrapper__books(:items="books")
</template>

<script>
import Tags from './components/Tags.vue';
import axios from 'axios';
import Library from "./components/Library";

export default {
  name: 'App',
  data() {
    return {
      categories: null,
      books: null
    }
  },
  components: {
    Library,
    Tags
  },
  mounted() {
    axios
        .post('https://webdev.modumlab.com/api/book/categories')
        .then(response => {
          this.categories = response.data.data.list;
        });
  },
  computed: {
    updateBooks: function() {
      return this.booksUpdate();
    }
  },
  methods: {
    booksUpdate() {
      axios
          .post('https://webdev.modumlab.com/api/book/list', {
            categories: [10111],
            page: 1
          })
          .then(response => {
            this.books = response.data.data.list;
          });
    }
  }
}
</script>

<style lang="scss">
  .wrapper {
    width: 70%;
    margin: 0 auto;
    padding: 50px 0 50px;

    &__books {
      margin-top: 20px;
    }
  }
</style>
