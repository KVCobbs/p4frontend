<template>
  <div class = "login">
     <b-field label="Username"
            type="is-success"
            message="This username is available">
            <b-input v-model = "username"></b-input>
        </b-field>

        <b-field label="Password">
            <b-input type="password"
                 v-model="password"
                password-reveal>
            </b-input>
        </b-field>
    <br/>
    <button class="button is-info" @click="handleLogin">Log In</button>
  </div>
</template>
<script>
export default {
  name:'Login',
  data: function(){
    return{
       username:'',
        password: ''
    };
  },
 methods: {
    handleLogin: function(){
      fetch(`${this.$route.query.URL}/users/users/login/`,{
        method: 'post',
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          username: this.username,
          password: this.password,
        }),
      })
      .then((response) => response.json())
      .then((data) =>
      this.$emit('loggedIn',data.token)
         // console.log(data)
      )
    },
  },
};
</script>

//Styling below
<style>
.login {
  width: 50%;
  margin: 10px auto;
}
</style>
