<template>
  <div class="user">
    <h1>{{ user.username }}</h1>
      <div class="info">
        <div>
          <p v-for="info in userInfo"><span>{{info.label}}:</span><span>{{info.value}}</span></p>
        </div>
        <div class="company">
          <strong>{{ user.company.name }}</strong><br>
          <p>{{ user.company.catchPhrase }}</p>
          <p>{{ user.company.bs }}</p>
        </div>
      </div>
      <div class="map">
        <iframe width="100%" height="450" frameborder="0" style="border:0" src="https://www.google.com/maps/embed/v1/place?q=40.7127837,-74.0059413&amp;key=AIzaSyB_GNwPXHh5X-KZ_H72hOp4kKlxAHBg_VI"></iframe>
      </div>
      <div class="album-list">
        <h2>Albums created by {{user.username}}</h2>
        <div v-for="album in albums">
          <router-link :to="'/album/' + album.id">{{album.title}}</router-link>
        </div>
      </div>
  </div>
</template>

<script>
/*
address
company
email
id
name
phone
username
website
*/
export default {
  data () {
    return {
      user: { company: {} },
      userInfo: [],
      albums: []
    }
  },
  created: function() {
    this.$http.get('http://jsonplaceholder.typicode.com/users/'+this.$route.params.id).then(
      response => {
        this.user = response.body;
        this.userInfo = [
          { label: "Name", value: this.user.name },
          { label: "Phone", value: this.user.phone },
          { label: "Email", value: this.user.email },
          { label: "Website", value: this.user.website },
          { label: "City", value: this.user.address.city },
        ]
      },
      response => {

      }
    );
      this.$http.get('http://jsonplaceholder.typicode.com/users/'+this.$route.params.id+'/albums').then(
        response => {
          this.albums = response.body;
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

.wrapper {
  display: flex;
  flex-flow: row;
}

.map {
  width: 70%;
  margin: auto;
}

.info {
  display: flex;
  width: 100%;
  justify-content: space-between;
  margin-bottom: 40px;
}

.info p { display: flex; justify-content: space-between; }

.info p span:first-child {
  font-weight: bold;
  padding-right: 100px;
}

a {
  color: #42b983;
}
</style>
