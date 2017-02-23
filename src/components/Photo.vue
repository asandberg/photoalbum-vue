<template>
  <div class="hello">
    <h1>{{ photo.title }}</h1>

      <img v-bind:src="photo.url" class="photo" />
      <p><router-link :to="'/album/' + this.photo.albumId">Album</router-link></p>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'photo',
  data () {
    return {
      photo: {}
    }
  },
  created: function() {
    this.$http.get('http://jsonplaceholder.typicode.com/photos/' + this.$route.params.id).then(
      response => {
        this.photo = response.body;
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
  margin: 0 20px;
}

.photo {
  max-width: 80%;
  display: block;
  margin: auto;
}

p {
  text-align: center;
}

a {
  color: #42b983;
}
</style>
