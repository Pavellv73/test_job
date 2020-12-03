<template lang="pug">
div
  Loader(v-if="isLoading")
  section.wrapper
    Tags.wrapper__categories(
      :tags="categories"
      @filter="this.getBooks"
    )
    Library.wrapper__books(
      :items="books"
      v-if="!isLoading"
    )
    ButtonMore.wrapper__button(
      :onClick="showMore"
      v-if="counterBooks > 10"
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
      counterBooks: 0,
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
          this.categories = values[0].data.data.list;
          this.getBooks(values[0].data.data.list);
          this.isLoading = false;
        })
        .catch(error => {
          this.isLoading = false;
          console.log(error, "error promise tags");
        });
  },
  methods: {
    getTags() {
      return axios.post(
          'https://webdev.modumlab.com/api/book/categories',
          {}
      );
    },
    getBooks(tags) {
      this.isLoading = true;
      let idArray = [];
      if (tags.length > 1) {
        tags.forEach(i => {
          idArray.push(i.id)
        })
      } else {
        idArray.push(tags)
      }

      axios.post('https://webdev.modumlab.com/api/book/list', {
        categories: idArray,
        page: 1
      })
          .then(values => {
            this.books = values.data.data.list;
            this.counterBooks = values.data.data.list.length;
            this.isLoading = false;
          })
          .catch(error => {
            console.log(error, "error getBooks");
            this.isLoading = false;
          });
    },
    showMore() {
      console.log(this.books, 'books');
      // this.getBooks();
    }
  }
}
</script>

<style lang="scss">
#app {
  width: 100%;
  height: 100%;
  position: relative;
}

.wrapper {
  width: 70%;
  margin: 0 auto;
  padding: 50px 0 50px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;

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
