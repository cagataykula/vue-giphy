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
  margin: 10px;
  width: 250px;
  height: 250px;
  border: 1px solid;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.gif {
  width: 200px;
  transition: all .3s ease;
  height: 200px;
}
.gif:hover{
    transform: scale(1.1, 1.1);
}

</style>
