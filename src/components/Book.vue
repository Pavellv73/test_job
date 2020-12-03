<template lang="pug">
div.book
  div.book__wrapper
    div.book__picture
      img(:src="image", :alt="title")
    div.book__info
      h3.book__title {{title}}
      span.book__description {{sliceDesc}}
      span.book__author {{author}}
      span.book__year {{year}}
</template>

<script>
export default {
  name: "Book",
  data() {
    return {
      sliceDesc: ''
    }
  },
  props: {
    image: String,
    title: String,
    author: String,
    description: String,
    year: String,
  },
  mounted() {
    this.textSlice();
  },
  methods: {
    textSlice() {
      const size = 100;
      const bookDesc = this.description;

      if (bookDesc.length > size) {
        this.sliceDesc = bookDesc.slice(0, size) + ' ...';
      }
    }
  }
}
</script>

<style lang="scss">
.book {
  padding: 5px;

  &__wrapper {
    height: 100%;
    border-radius: 10px;
    border: 1px solid black;
    overflow: hidden;
  }

  &__picture {
    width: 100%;
    height: 150px;
    overflow: hidden;
    object-fit: contain;

    img {
      width: 100%;
    }
  }

  &__info {
    margin-top: 10px;
    padding: 0 15px 20px;
  }

  &__title {
    font: 600 16px/18px Arial, sans-serif;
  }

  &__description,
  &__author,
  &__year {
    display: block;
    margin-top: 5px;
  }
  
  &__description {
    font: 300 14px/16px Arial, sans-serif;
  }

  &__author,
  &__year {
    font: 600 12px/14px Arial, sans-serif;
  }
}
</style>