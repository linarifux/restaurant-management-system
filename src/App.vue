<template>
  <div id="nav">
    <router-link to="/">Home</router-link> | <router-link to="/about">About Us</router-link>
  </div>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  margin-top: 4rem;
  margin-bottom: 2rem;
  padding-left: .5rem;
  padding-right: .5rem;
  font-size: 20px;
  font-weight: 700;
  color: #ffffff;
}

#nav a {
  font-weight: bold;
  margin: 0 1rem;
  color: #ffffff;
  font-size: 30px;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

* {
  margin: 0;
  padding: 0;
}

body {
  background: #474787;
}

img {
  height: 300px;
  width: 450px;
  border: 5px solid #474787;
  border-radius: 2px;
}

.container {
  max-width: 80vw;
  margin: 5rem auto;
}

@media screen and (max-width: 768px) {
  img {
    height: 200px;
    width: 250px;
    border: 2px solid #474787;
  border-radius: 2px;
  }
}
</style>
