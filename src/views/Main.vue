<template>
  <div class="main">
 <ul>

   <li v-for="insults of insults" v-bind:key="insults.id" >
      <b-message title="Most recent insult" type="is-dark" has-icon icon="account" aria-close-label="Close message">
        {{insults}}
        <br>

        <b-button v-bind:id ="insults" @click="()=> deleteInsult(insults.id)" rounded>Delete</b-button>
        <b-button rounded v-model:id="editid" @click="(insult.id)">Edit</b-button>

        </b-message>


             <b-field label="Edit">
            <b-input type="text" v-model="editmessage" maxlength="30" rounded>Edit</b-input>
        </b-field>
        <br>
   </li>
 </ul>


    <br>
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
      editmessage: "",
      editid: null
    };
  },
  created: function() {
    this.getInsult()
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
        body: JSON.stringify({text: this.message,user:2}),
      }).then(() => {
        this.getInsult();
      });
    },
    getInsult: function(){
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
    });
    },
    deleteInsult: function(id){
      const token = this.$route.query.tokens
      //const = event.target.id
       fetch(`http://localhost:8000/api/insults/${id}/`, {
        method: 'delete',
        headers: {
          authorization: `JWT ${token}`,
          "Content-Type":"application/json"
        },
    })
      .then(() => {
        this.getInsult()
      });
    },
    editSelect: function(id,content){
      this.editid = id
      this.editmessage = content
    },
    editInsult: function(id){
      const token = this.$route.query.tokens
      //const = event.target.id
       fetch(`http://localhost:8000/api/insults/${id}/`, {
        method: 'delete',
        headers: {
          authorization: `JWT ${token}`,
          "Content-Type":"application/json"
        },
    })
      .then(() => {
        this.getInsult()
      })
}
</script>

<style>
div.main {
  width: 50%;
  min-width: 300px;
  margin: 10px auto;
}
</style>