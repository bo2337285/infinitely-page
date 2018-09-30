<template>
  <div id="app">
    <span class="tips"># 上拖翻页,下拖上一页</span>
    <router-view />
  </div>
</template>

<script>

export default {
  name: 'App'
}
</script>

<style  lang="stylus">
body, html
  margin 0
  padding 0
  width 100%
  height 100%
  #app
    width 100%
    height 100%
    font-family 'Avenir', Helvetica, Arial, sans-serif
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale
    text-align center
    color #2c3e50
    .tips
      position absolute
      color #ddd
</style>
