<template lang="pug">
section.wrapper
  Loader(v-if="isLoading")
  Tags.wrapper__categories(
    :tags="categories"
    v-model="updateBooks"
    @filter="this.getBooks"
  )
  Library.wrapper__books(
    :items="books"
    v-if="!isLoading"
  )
  ButtonMore.wrapper__button(
    :onClick="showMore"
    v-if="conterBooks > 10"
  ) Загрузить ещё
</template>

<script>
import axios from 'axios';
import Loader from "@/components/Loader";
import Tags from '@/components/Tags.vue';
import Library from "@/components/Library";
import ButtonMore from "@/components/ButtonMore";

export default {
  name: 'App',
  data() {
    return {
      isLoading: false,
      categories: null,
      books: null,
      conterBooks: 0,
      filter: null
    }
  },
  components: {
    Loader,
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
          this.isLoading = false;
        })
        .catch(() => {
          console.log("error promise tags");
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
    async getBooks(tags) {
      console.log(tags);
      let idArray = [];
      if (tags.length > 1) {
        tags.forEach(i => {
          idArray.push(i.id)
        });
      } else {
        idArray.push(tags);
      }

      this.isLoading = true;
      await Promise.all([axios.post('https://webdev.modumlab.com/api/book/list', {
            categories: idArray,
            page: 1
          })])
          .then(values => {
            this.books = values[0].data.data.list;
            this.conterBooks = values[0].data.data.list.length;
            this.isLoading = false;
          })
          .catch(() => {
            console.log("error getBooks");
            this.isLoading = false;
          });
    },
    showMore() {
      console.log(this.books);
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
