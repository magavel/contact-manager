<template>
  <div id="app">
    <router-link class="m-3" :to="{name: 'home'}" exact>Home</router-link>
    <router-link class="m-3" :to="{name: 'about'}">LinkTitle</router-link>
    <router-view/>
  </div>
</template>

<script>


export default {};
</script>

<style>
.router-link-active {
  color: blueviolet;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
