<template>
  <div class="header">
     <b-navbar>
      <template slot="brand">
        <b-navbar-item tag="router-link" :to="{ path: '/' }">
          <span class = "logo">BITTER</span>
        </b-navbar-item>
      </template>

     <!-- <template slot="start">
        <b-navbar-item href="#">
          <router-link to="/">Home</router-link>
        </b-navbar-item>
        <b-navbar-item href="#">
          <router-link to="/Page2">About</router-link>
        </b-navbar-item>
        <b-navbar-dropdown label="Info">
          <b-navbar-item href="#">
            About
          </b-navbar-item>
          <b-navbar-item href="#">
            Contact
          </b-navbar-item>
        </b-navbar-dropdown>
      </template> -->

      <template slot="end">
        <b-navbar-item tag="div">
          <div class="buttons">
            <a class="button is-primary">
              <strong>Sign up</strong>
            </a>
            <a class="button is-light">
              <router-link :to= "{ name: 'Login', query: { URL: this.URL }}" v-bind:URL="URL" v-if="!loggedIn"><button class="button is-info">Log out</button></router-link>
               <!-- <button v-if = "!loggedIn" class= "is-primary" click="logout">Logout</button> -->
            </a>
          </div>
        </b-navbar-item>
      </template>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: ['URL','loggedIn'],
  methods: {
    logout: function(){
      this.$emit()('logout')
    }
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Fredoka+One&display=swap');

.header {
    width: 90%;
    margin: 10px auto
}

span.logo{
  font-family: Fredoka One,serif;
  font-size: 2em;
  color: royalblue;
}


</style>
