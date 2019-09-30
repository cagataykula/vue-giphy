<template>
  <div>
    <div class="gifs">
      <GifCard
        v-for="item in gifs"
        :key="item.id + lastKey"
        :src="item.images.fixed_height.url"
      />
    </div>
    <infinite-loading @infinite="getNewGifs"></infinite-loading>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
import GifCard from '@/components/GifCard.vue';
import InfiniteLoading from 'vue-infinite-loading';

export default {
  name: 'home',
  data(){
    return{
      gifs: [],
      gifCount: 0,
      lastKey: ''
    }
  },
  methods: {
    getNewGifs: function ($state) {
      console.log('state ', $state);
      axios.get(`https://api.giphy.com/v1/gifs/trending?api_key=nbAmrxeq4s6nOvEA4CUtgiFHNGa7JCMn&limit=20&offset=${this.gifCount}`)
        .then(response => {
          if (response.data.data.length) {
            this.gifCount += 20;
            if(this.lastKey != response.data.data[response.data.data.length - 1].id) {
              response.data.data.forEach(item => {
                this.gifs.push(item);
              });
              this.lastKey = response.data.data[response.data.data.length - 1].id;
            }
            $state.loaded();
          } else {
            $state.complete();
          }
        });
    },
  },
  components: {
    GifCard,
    InfiniteLoading,
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
