<template lang="pug">
  #app
    .widget-user-info
      .user-info__basic
        img(:src="data.avatar_url")
        div
          .basic__name {{ data.name }}
          .basic__bio {{ data.bio }}
          .basic__loaction {{ data.location }}
      .user-info__stat
    .widget-repo-info
    .widget-contact
  
</template>

<script>
  import axios from 'axios'
const user = "dingdingbai"

export default {
  name: 'app',
  data() {
    return {
      data:null,
    }
  },
  created() {
    axios.get("https://api.github.com/users/" + user)
      .then(res=>{
        this.data = res.data
        console.log(this.data)
      })
  }
}
</script>

<style lang="stylus">
#app 
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 400px;
  height: 600px;
  margin: auto;
  border: solid 1px #ccc;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
.user-info__basic
  display: flex
  align-items: center
  > img
    width: 80px;
    border-radius: 50%;
</style>
