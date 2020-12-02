<template lang="pug">
section.wrapper
  Tags.wrapper__categories(:tags="categories" v-model="updateBooks")
  Library.wrapper__books(:items="books")
<!--  ButtonMore.wrapper__button(-->
<!--    :onClick="showMore"-->
<!--    v-if="this.books.length > 10"-->
<!--  ) Загрузить ещё-->
</template>

<script>
import axios from 'axios';
import Tags from '@/components/Tags.vue';
import Library from "@/components/Library";
import ButtonMore from "@/components/ButtonMore";

export default {
  name: 'App',
  data() {
    return {
      isLoading: false,
      categories: null,
      books: null
    }
  },
  components: {
    Tags,
    Library,
    ButtonMore
  },
  mounted() {
    this.isLoading = true;
    Promise.all([this.getTags()])
        .then(values => {
          this.categories = values[0];
          this.getBooks(values[0])
        })
        .catch(() => {
          console.log(0);
          this.isLoading = false;
        });
  },
  computed: {
    updateBooks: function() {
      return console.log('updateBooks');
      // return this.getBooks();
    }
  },
  methods: {
    async getTags() {
      const response = await axios.post(
          'https://webdev.modumlab.com/api/book/categories',
          {}
      );
      return response.data.data.list;
    },
    getBooks(tags) {
      let idArray = [];
      tags.forEach(i => {
        idArray.push(i.id)
      });

      console.log(idArray);

      axios
          .post('https://webdev.modumlab.com/api/book/list', {
            categories: idArray,
            page: 1
          })
          .then(response => {
            this.books = response.data.data.list;
          });
    },
    showMore() {
      console.log(this.books.length)
    }
  }
}
</script>

<style lang="scss">
.wrapper {
  width: 70%;
  margin: 0 auto;
  padding: 50px 0 50px;
  display: flex;
  flex-direction: column;
  justify-content: center;

  &__books {
    margin-top: 20px;
    margin-bottom: 50px;
  }

  &__button {
    width: 250px;
    margin: 0 auto;
    padding: 10px 15px;
    background-color: hotpink;
    transition: background-color 0.3s ease;
    color: white;
    border-radius: 10px;

    &:hover {
      background-color: deeppink;
    }
  }
}
</style>
