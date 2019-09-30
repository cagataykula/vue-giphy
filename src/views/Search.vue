<template>
  <div class="pageWrapper">
    <div class="top">
      <input type="text" v-model="query" v-on:keyup.enter="search()" />
      <button @click="search()">Search</button>
    </div>
    <div class="gifs">
      <GifCard v-for="item in gifs" :key="item.id + lastKey" :src="item.images.fixed_height.url" />
    </div>
    <p v-if="noResult">No results found for {{query}}</p>
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
      query: '',
      noResult: false
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
            this.noResult = false;
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
          } else {
            this.noResult = true;
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
  },
  watch: {
    query: function (newValue) {
      this.noResult = false;
    }
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