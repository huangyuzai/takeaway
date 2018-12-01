<template>
  <div id="app">
    <app-header :seller="this.seller"></app-header>
    <div class="navList border-1px">
      <div class="goods nav-item">
        <router-link to='/'>商品</router-link>
      </div>
      <div class="rating nav-item">
        <router-link to='/rating'>评价</router-link>
      </div>
      <div class="seller nav-item">
        <router-link to='/seller'>商家</router-link>
      </div>
    </div>
    <router-view/>
  </div>
</template>

<script>
import AppHeader from 'components/header/AppHeader'
import axios from 'axios'
export default {
  name: 'App',
  components: {
    AppHeader
  },
  data () {
    return {
      goods: [], // 商品数据
      ratings: [], // 评价数据
      seller: {} // 商家数据
    }
  },
  methods: {
    // 请求数据
    getHeaderData () {
      axios.get('/api/data.json')
        .then(this.getHeaderSucc)
    },
    // 请求成功的回调
    getHeaderSucc (res) {
      const data = res.data
      this.goods = data.goods
      this.ratings = data.ratings
      this.seller = data.seller
      // console.log(this.seller)
      // console.log(data)
    }
  },
  // 页面加载完成即请求数据
  mounted () {
    this.getHeaderData()
  }
}
</script>

<style lang='stylus' scoped>
@import 'common/stylus/mlxin.styl'

#app
  .navList
    display: flex
    height: 40px
    line-height: 40px
    border-1px(rgba(7,17,27,.1))
    .nav-item
      flex: 1
      text-align: center
      a
        display: block
        font-size: 14px
        color: rgb(77,85,93)
      .router-link-exact-active
        color: rgb(240,20,20)
</style>
