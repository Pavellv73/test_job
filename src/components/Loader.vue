<template lang="pug">
i.preloader
</template>

<script>
export default {
  name: "Loader"
}
</script>

<style lang="scss">
.preloader {
  display: block;
  width: 50px;
  height: 50px;
  border: 3px solid deeppink;
  border-bottom-color: #fff;
  border-radius: 50%;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  animation: spin .75s infinite linear;
}

@keyframes spin {
  100% {
    transform: rotate(360deg);
  }
}
</style>