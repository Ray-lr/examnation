<template>
  <div id="app">
    <img  height="200" width="200" src="./assets/avatar.jpg"><br>
    作者: Ray
    <h1> 第二套考题</h1>
    <Home/>
  </div>
</template>

<script>
import Home from './components/Home'

export default {
  name: 'App',
  components: {
    Home
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
