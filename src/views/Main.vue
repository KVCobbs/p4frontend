<template>
  <div class="main">
 <ul>
   <li v-for="insults of insults" v-bind:key="insults">
      <b-message title="Dark with custom icon" type="is-dark" has-icon icon="account" aria-close-label="Close message">
        {{insults}}
        </b-message>
   </li>
 </ul>
      <b-field label="New Status">
            <b-input maxlength="200" v-model="message" type="textarea"></b-input>
        </b-field>
        <b-button rounded @click="newInsult">Submit</b-button>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Main',
  data: function(){
    return {
      insults: [],
      message: "",
    }
  },
  created: function() {
    this.getInsults()
  },
   // const {URL} = this.$route.query.URL
   // const token = this.$route.query.tokens

   // console.log(this.$route.query)
   // fetch(`http://localhost:8000/api/insults/`, {
   //   method: 'get',
    //  headers: {
    //    authorization: `JWT ${token}`,
        //"Content-Type":"application/json"
     //   }
     // })
   // .then(response => response.json())
   // .then(data => {
     //   this.insults = data
     // console.log(URL)
   // })
  //}
  methods: {
    newInsult: function(){
       // const {URL} = this.$route.query.URL
        const token = this.$route.query.tokens
      console.log("hi",this.message)
      fetch(`http://localhost:8000/api/insults/`, {
      method: 'post',
      headers: {
        authorization: `JWT ${token}`,
        "Content-Type": 'application/json',
        },
        body: JSON.stringify({text: this.message}),
      }).then(() => {
        this.getInsults();
      });
    },
    getInsults: function(){
        //const {URL} = this.$route.query.URL
        const token = this.$route.query.tokens

      fetch(`http://localhost:8000/api/insults/`, {
        method: 'get',
        headers: {
        authorization: `JWT ${token}`,
        //"Content-Type":"application/json"
         },
       })
    .then(response => response.json())
    .then(data => {
      this.insults = data
      //console.log(URL)
    })
    }
  }
}
</script>