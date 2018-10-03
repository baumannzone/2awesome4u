<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/custom">Custom</router-link>
    </div>
    <router-view/>
    <div class="footer">
      <p><a href="https://twitter.com/baumannzone" target="_blank">@baumannzone</a> | <a href="https://github.com/baumannzone/2awesome4u" target="_blank">Github</a></p>
    </div>
  </div>
</template>

<style lang="stylus">
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-bottom 100px

#nav
  a
    font-weight bold
    color #2c3e50
    &.router-link-exact-active
      color #42b983
.footer
  position fixed
  width 100%
  bottom 0
  left 0
  background-color #f1f1f1
  a
    color #aaa
    &:hover
      color #777

</style>
