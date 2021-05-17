<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Login/Logout</router-link> |
      <router-link to="/about">Voting</router-link>
    </div>
    <router-view />
  </div>
</template>
<script>
// @ is an alias to /src

export default {
  name: "Home",
  components: {},
}
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {
  background-color: #0a1128;
}
#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #70a0cf;
    margin: 4rem;
    font-size: 2rem;
    text-decoration: none;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
