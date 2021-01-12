<template>
  <div id="app">
    <Header/>
    <Weather/>
    <Footer/>
    
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld';
import Header from './components/Header';
import Weather from './components/Weather';
import Footer from './components/Footer';


export default {
  name: 'App',
  components: {
    // HelloWorld,
    Header,
    Weather,
    Footer
  }
}
</script>

<style>
*{
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
