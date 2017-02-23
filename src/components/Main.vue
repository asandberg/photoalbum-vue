<template>
  <div>
    <ul class="photo-list">
      <li v-for="photo in photos">
        <router-link :to="'/photo/' + photo.id"><img v-bind:src="photo.thumbnailUrl" class="photo" /></router-link>
      </li>
    </ul>
    <div class="loader" v-if="loading"><img v-bind:src="'static/ripple.svg'" /></div>
  </div>
</template>

<script>
import config from '../config'

export default {
  data () {
    return {
      photos: [],
      lastLoadedPage: 0,
      loading: false
    }
  },
  created: function() {
    this.load(0);
    window.addEventListener('scroll', this.onScroll);
  },
  destroyed() {
    window.removeEventListener('scroll', this.onScroll);
  },
  methods: {
    onScroll: function(event) {
      if(window.scrollY + window.innerHeight - this.$el.offsetTop >= this.$el.scrollHeight - 300) {
        this.load(this.lastLoadedPage + 1);
      }
    },
    load: function(page) {
      if(this.loading)
        return;
      this.loading = true;
      this.$http.get(`${config.dataSourcePath}/photos/?_limit=${config.photoLimit}&_page=${page}`).then(
        response => {

          // Load album images
          // The images are pre-loaded before they are added to the DOM
          let imageCount = 0;
          response.body.forEach((item, index) => {
            let img = new Image();
            imageCount++;
            this.loading = true;
            img.onload = () => {
              item.thumbnailUrl = img.src;
              this.photos.push(item);
              imageCount--;

              if(imageCount <= 0)
                this.loading = false;
            }
            img.src = item.thumbnailUrl;
          });

          if(response.body.length == 0)
            this.loading = false;
          this.lastLoadedPage = page;
        },
        response => {
          console.error(response);
          this.loading = false;
        }
      );
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.loader {
  text-align: center;
  width: 100%;
  margin-top: -50px;
  position: relative;
  z-index: 1;
  transition: width 1s, height 1s;
}
</style>
