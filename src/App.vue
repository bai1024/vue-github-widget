<template lang="pug">
#app(v-if="data && repos")
  .widget-user-info
    .user-info__basic
      img(:src="data.avatar_url")
      div
        .basic__name {{ data.name }}
        .basic__bio {{ data.bio }}
        .basic__loaction {{ data.location }}
    .user-info__stat
        .stat__follower 
          span {{ data.followers }}
          span Follower
        .stat__following 
          span {{ data.following }}
          span Following
        .stat__repos 
          span {{ data.public_repos }}
          span  Repostories
  hr
  .widget-repo-info
    p Top repositories
    repos-item(
      v-for="item in repos.slice(0, 3)"
      :item="item"
    )
  .widget-bottom 
    .follow-btn 
      a(href="https://github.com/" + user) Follow
    .update-time Update: {{ data.updated_at | timeago }}

</template>

<script>
import axios from 'axios'
import timeago from "timeago.js"
import ReposItem from "@/components/repos-item"

// const user = "dingdingbai"

export default {
  name: 'app',
  data() {
    return {
      data:null,
      repos:null,
      user: "dingdingbai"
    }
  },
  created() {
    axios.get("https://api.github.com/users/" + this.user)
      .then(res=>{
        this.data = res.data
      }),
    axios.get("https://api.github.com/users/"+ this.user + "/repos")
      .then(res => {
        this.repos = res.data.sort(function(a,b){
          return b.stargazers_count - a.stargazers_count
        })
      })
  },
  filters:{
    timeago(t){
      return timeago().format(t)
    }
  },
  components: {
    ReposItem
  }
}
</script>

<style src='normalize.css'></style>
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
    flex: 2
    padding: 10px
    width: 80px;
    border-radius: 50%
  > div
    flex: 5
    width: 270px
    text-align: center

.basic__name
  font-size: 25px

.basic__bio
  color: #4078C0
  font-size: 14px
  margin: 10px 0

.basic__loaction
  font-size: 14px

.user-info__stat
  display: flex
  align-items: center
  justify-content: space-around
  font-size: 16px
  font-weight: 600
  div
    span
      display: block
      &:first-child
        color: #4078C0
        
.widget-repo-info
  p
    font-weight: 600
        
.widget-bottom
  display: flex
  align-items: center
  justify-content: space-around

.follow-btn
  padding: 5px 30px
  background: #ddd
  > a
    color: #4078c0;
    text-decoration: none
</style>
