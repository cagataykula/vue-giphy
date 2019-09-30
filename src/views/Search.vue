<template>
  <div class="pageWrapper">
    <div class="top">
      <input type="text" v-model="query" v-on:keyup.enter="search()" />
      <button @click="search()">Searh</button>
    </div>
    <div class="gifs">
      <GifCard v-for="item in gifs" :key="item.id + lastKey" :src="item.images.fixed_height.url" />
    </div>
    <button v-if="gifs.length" @click="loadMore()">Load More</button>
  </div>
</template>

<script>
import axios from 'axios';
import GifCard from '@/components/GifCard.vue';

export default {
  data() {
    return {
      gifs: [],
      gifCount: 0,
      lastKey: '',
      query: ''
    };
  },
  methods: {
    search: function() {
      this.gifs = [];
      axios.get(
          `https://api.giphy.com/v1/gifs/search?api_key=nbAmrxeq4s6nOvEA4CUtgiFHNGa7JCMn&limit=20&offset=${this.gifCount}&q=${this.query}`
        )
        .then(response => {
          if (response.data.data.length) {
            this.gifCount = 20;
            if (
              this.lastKey !=
              response.data.data[response.data.data.length - 1].id
            ) {
              response.data.data.forEach(item => {
                this.gifs.push(item);
              });
              this.lastKey =
                response.data.data[response.data.data.length - 1].id;
            }
          }
        });
    },
    loadMore: function() {
        axios.get(
          `https://api.giphy.com/v1/gifs/search?api_key=nbAmrxeq4s6nOvEA4CUtgiFHNGa7JCMn&limit=20&offset=${this.gifCount}&q=${this.query}`
        )
        .then(response => {
          if (response.data.data.length) {
            this.gifCount += 20;
            if (
              this.lastKey !=
              response.data.data[response.data.data.length - 1].id
            ) {
              response.data.data.forEach(item => {
                this.gifs.push(item);
              });
              this.lastKey =
                response.data.data[response.data.data.length - 1].id;
            }
          }
        });
    }
  },
  components: {
      GifCard
  }
};
</script>

<style scoped>
.gifs {
  display: flex;
  flex-direction: row;
  justify-content: center;
  padding: 20px;
  flex-wrap: wrap;
}

.pageWrapper {
  display: flex;
  justify-content: center;
  flex-direction: column;
}

.top {
  display: flex;
  justify-content: center;
  flex-direction: row;
}
</style>