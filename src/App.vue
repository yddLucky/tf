<template>
  <div id="app">
    <m-head :backFlag="backFlag"></m-head>
    <router-view></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
  import MHead from 'components/m-header/m-header'
  import {isiphoneX} from 'common/js/util'

  export default {
    data(){
      return {
        backFlag: true
      }
    },
    components: {
      MHead
    },
    mounted() {
      // 解决安卓手机输入框被遮挡问题
      if (/Android/gi.test(navigator.userAgent)) {
        window.addEventListener('resize', function () {
          if (document.activeElement.tagName == 'INPUT' || document.activeElement.tagName == 'TEXTAREA') {
            window.setTimeout(function () {
                document.activeElement.scrollIntoViewIfNeeded()
            }, 0)
          }
        })
      }
    },
    watch:{
      $route(to,from){
        if(to.path === '/preview') {
          this.backFlag = false
        }else{
          this.backFlag = true
        }
        isiphoneX()
      }
    }
  }
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
</style>