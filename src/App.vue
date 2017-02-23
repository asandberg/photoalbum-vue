<template>
  <div id="app">
    <header><router-link to="/"><h2>Vue Photo Album</h2></router-link></header>
    <div id="main"><router-view></router-view></div>
    <footer><p>What are cookies made of?</footer>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style>

html, body {
  margin: 0; padding: 0;
}
#main, header a, header h2 {
  max-width: 1100px;
}

h1, h2 {
  text-transform: capitalize;
  text-align: center;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  padding-bottom: 4rem;
  position: relative;
}

#main {
  margin-top: 60px;
  margin: 50px auto;
}

header {
  font-size: 1.5em;
  background-color: rgb(34, 154, 42);
  margin: 0;
  padding: 0.5em;
}

header a, header h2 {
  padding: 0;
  margin: auto;
  text-decoration: none;
  color: rgb(246, 246, 246);
}

footer {
  background-color: rgb(11, 55, 14);
  color: rgb(246, 246, 246);
  padding: 1.5em;
  text-align: center;
  position: absolute;
  width: 100%;
  box-sizing: border-box;
  bottom: 0;
  height: 4rem;
}

.photo-list {
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  list-style-type: none;
}

.photo-list li {
  margin: 14px;
}

.photo {
  background-color: white;
  padding: 12px;
  border: 0px solid rgb(198, 198, 198);
  box-shadow: 4px 4px 4px 0px hsla(0,0%,30%, 0.22);
  box-sizing: border-box;
}

@media (min-width: 1000px) {
  li:nth-child(7n+1) .photo { transform: rotate(3deg); }
  li:nth-child(7n+2) .photo { transform: rotate(-1deg); }
  li:nth-child(7n+3) .photo { transform: rotate(-2deg); }
  li:nth-child(7n+4) .photo { transform: rotate(5deg); }
  li:nth-child(7n+5) .photo { transform: rotate(1deg); }
  li:nth-child(7n+6) .photo { transform: rotate(5deg); }
  li:nth-child(7n+7) .photo { transform: rotate(-4deg); }
}

footer p { padding: 0; margin: 0; }

@media (max-width: 600px) {
  .photo-list li {
    width: 40%;
  }
  .photo {
    width: 100%;
  }
}
</style>
