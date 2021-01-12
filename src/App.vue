<template>
  <div id="app">
    <Header/>
    <Weather/>
    <Footer/>
    
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import Header from './components/Header.vue';
import Weather from './components/Weather.vue';
import Footer from './components/Footer.vue';


export default {
  name: 'App',
  components: {
    HelloWorld,
    Header,
    Weather,
    Footer
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
