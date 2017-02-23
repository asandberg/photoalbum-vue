<template>
  <div class="hello">
    <h1>{{ album.title }}</h1>
    <h2>by <router-link :to="'/user/' + album.userId">{{ album.userId }}</h2>
    <ul class="photo-list">
      <li v-for="photo in photos">
        <router-link :to="'/photo/' + photo.id"><img v-bind:src="photo.thumbnailUrl" class="photo" /></router-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data () {
    return {
      photos: [],
      album: {}
    }
  },
  created: function() {
    this.$http.get('http://jsonplaceholder.typicode.com/albums/'+this.$route.params.id).then(
      response => {
        console.log(response);
        this.album = response.body;
      },
      response => {

      }
    );
    this.$http.get('http://jsonplaceholder.typicode.com/album/'+this.$route.params.id+'/photos').then(
      response => {
        console.log(response);
        this.photos = response.body;
      },
      response => {

      }
    );
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

a {
  color: #42b983;
}
</style>
