<template>
  <div id="app">
    <div id="nav">
      <Header v-bind:URL="URL" v-bind:loggedIn = "loggedIn" @logout="logout"/>

      
    </div>
    <router-view @loggedIn = "login($event)"/>
    <Footer/>
  </div>
</template>

<script>
import Header from './components/Header'
import Footer from './components/Footer'

export default {
  name: 'App',
  components: {
    Header,
    Footer
  },
  data: function(){
    return {
      loggedIn:false,
      tokens: {},
      URL: 'http://localhost:8000'
    }
  },
  methods: {
    login: function(event){
      console.log("event heard")
      this.loggedIn = false
      this.tokens = event
      this.$router.push({ path: '/main', query: { tokens: this.tokens, URL: this.URL } });
      console.log(this.tokens)
     // this.$router.push("/main")
    },
    logout: function(){
      this.loggedIn = false
      this.tokens = {};
    }
  }
};
</script>

<style>
body{
  color: royalblue;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 50px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
