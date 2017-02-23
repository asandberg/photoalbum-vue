<template>
  <div>
    <h1>Welcome!</h1>
    <ul class="photo-list">
      <li v-for="photo in photos">
        <router-link :to="'/photo/' + photo.id"><img v-bind:src="photo.thumbnailUrl" class="photo" /></router-link>
      </li>
    </ul>
    <div></div>
  </div>
</template>

<script>
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
      if(window.scrollY + window.innerHeight - this.$el.offsetTop >= this.$el.scrollHeight - 200) {
        this.load(this.lastLoadedPage + 1);
      }
    },
    load: function(page) {
      if(this.loading)
        return;
      this.loading = true;
      this.$http.get('http://jsonplaceholder.typicode.com/photos/?_limit=20&_page=' + page).then(
        response => {
          this.photos = this.photos.concat(response.body);
          this.lastLoadedPage = page;
          this.loading = false;
        },
        response => {
          this.loading = false;

        }
      );
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
  text-align: center;
}

a {
  color: #42b983;
}
</style>
