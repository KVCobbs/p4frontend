<template>
  <div class="main">
 <ul>
   <li v-for="Insults of insults" v-bind:key="insult.id">{(insult.text)}</li>
 </ul>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Main',
  data: function(){
    return {
      insults: []
    }
  },
  created: function(){
    const {tokens, URL} = this.$route.query

    fetch(`${URL}/api/insults/`, {
      method: 'get',
      headers: {
        authorization: `Bearer $(tokens.access)`
        }
      })
    .then(response => response.json())
    .then(data => {
        this.insults = data
    })
  }
}
</script>