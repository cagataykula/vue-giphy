<template>
  <div class="gifCardWrapper">
    <img
      :src="src"
      class="gif"
    >
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    src: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.gifCardWrapper {
  transition: all .3s ease;
  margin: 10px;
}
.gifCardWrapper:hover {
  transform: scale(1.1, 1.1);
}
.gif {
  width: 200px;
}
</style>
