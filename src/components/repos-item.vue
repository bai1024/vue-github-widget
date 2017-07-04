<template lang="pug">
  .repo-item
    .repo-item__name
      a(:href="item.html_url") {{ item.name }}
    .repo-item__language {{ item.language }}
    .repo-item__count ★ {{ item.stargazers_count }}
</template>

<script>
import timeago from "timeago.js"

export default {
  props:{
    item:{
      type: Object,
      required: true,
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
.repo-item
  padding: 15px
  display: flex
  justify-content: space-around
  align-items: center
  div 
    margin-bottom: 35px
    width: 33.3%
    text-align: left
    
.repo-item__name
  a
    color: #4078C0;
    text-decoration: none;
.repo-item__language
  padding-left: 55px
  
.repo-item__count
  padding-left: 60px
</style>
