<template>
  <div id="app">
    <div id="nav"></div>
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#nav {
  display:flex;
  height: 70px;
  border: 2px ridge black;
  background-color: #737b83;
  position: sticky;
  top: 5px;
  justify-content: center;
  align-content: center;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

#thingsToDo {
  color: white;
  font-weight: bold;
  font-size: 20px;
  margin-right: 10px;
  padding: 20px;
}
</style>
