<template>
  <div class="hello">
    <h2 class="label">Photo</h2>
    <h1>{{ photo.title }}</h1>

      <img v-bind:src="photo.url" class="photo" />
      <p><router-link :to="'/album/' + this.photo.albumId">Album</router-link></p>
    </ul>
  </div>
</template>

<script>
import config from '../config'
export default {
  name: 'photo',
  data () {
    return {
      photo: {}
    }
  },
  created: function() {
    this.$http.get(`${config.dataSourcePath}/photos/${this.$route.params.id}`).then(
      response => {
        this.photo = response.body;
      },
      response => { console.error(response); }
    );
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.photo {
  max-width: 80%;
  display: block;
  margin: auto;
}

p {
  text-align: center;
}
</style>
