<template>
  <div>
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link :to="{ path: '/goods'}" >商品</router-link>
        </div>
      <div class="tab-item">
        <router-link :to="{ path: '/ratings'}" >评论</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{ path: '/seller'}" >商家</router-link>
      </div>
    </div>
   <router-view></router-view>
  </div>

</template>
<script>
import header from './components/header/header'
// eslint-disable-next-line
const ErrOk = 0
export default {
  name: 'App',
  components: {
    'v-header': header
  },
  data() {
    return {
      seller:{

      }
    }
  },
  created(){
    this.$http.get('/api/seller').then(response => {
      // eslint-disable-next-line
      response = response.body
      if(response.errno === ErrOk){
        this.seller = response.data
      }
    })
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin.styl"
  .tab
    display: flex
    width: 100%
    height: 40px
    line-height: 40px
    // border-bottom: 1px solid rgba(7, 17, 27, 0.1)
    border-1px(rgba(7, 17, 27, 0.1))
    .tab-item
      flex: 1
      text-align: center
      & > a
        display: block
        font-size: 14px
        color: rgb(77, 85, 93)
        &.active
          color: rgb(240, 20, 20)
</style>
