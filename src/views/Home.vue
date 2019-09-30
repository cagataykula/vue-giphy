<template>
  <div class="gifs">
    <GifCard
      v-for="item in gifs"
      :key="item.id"
      :src="item.images.fixed_height.url"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
import GifCard from '@/components/GifCard.vue';

export default {
  name: 'home',
  data(){
    return{
      gifs: {}
    }
  },
  created: function () {
    axios.get('https://api.giphy.com/v1/gifs/trending?api_key=nbAmrxeq4s6nOvEA4CUtgiFHNGa7JCMn&limit=20')
      .then(response => response.data)
      .then((response) => {
        console.log(response);
        this.gifs = response.data;
      });
  },
  components: {
    GifCard,
  },
};
</script>

<style scoped>
.gifs {
  display: flex;
  justify-content: center;
  padding: 20px;
  flex-wrap: wrap;
}
</style>
