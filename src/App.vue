<template>
  <nav>
    <router-link to="/">Авторизация</router-link> |
    <router-link to="/analytics">Аналитика</router-link>
  </nav>
  <div class="container">
    <router-view />
  </div>
</template>

<style>
.container {
  width: 80%;
  max-width: 720px;
  margin: 0 auto;
}
#app {
  font-family: Roboto, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: #fdf5df;
  height: 100vh;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #123c69;
}

nav a.router-link-exact-active {
  color: #5ebec4;
}
</style>
