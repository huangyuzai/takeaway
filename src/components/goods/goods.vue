<template>
  <div class="Goods">
    <!-- 左边菜单 -->
    <div class="menu-wrapper">
      <ul class="menu-nav">
        <li class="menu-item" v-for="item of goods" :key="item.index">
          {{item.name}}
        </li>
      </ul>
    </div>
    <!-- 右边商品区 -->
    <div class="goods-wrapper"></div>
  </div>
</template>

<script>
import axios from 'axios'
const ERR_OK = 0 // 定义错误码
export default {
  name: 'Goods',
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      goods: [] // 商品数据
    }
  },
  mounted () {
    // 请求商品数据
    axios.get('/api/goods').then((res) => {
      const data = res.data
      if (data.errno === ERR_OK) {
        this.goods = data.data
      }
    })
  }
}
</script>

<style lang="stylus" scoped>
.Goods
  display: flex
  position: absolute
  top: 174px
  bottom: 50px
  width: 100%
  .menu-wrapper
    width: 80px
    flex: 0 0 80px
    background: #f3f5f7
    box-sizing: border-box
    .menu-nav
      .menu-item
        font-size: 12px
        color: rgb(7,17,27)
        font-weight: 200
        line-height: 14px
        height: 54px
        display: flex
        align-items: center
        border-bottom: solid 1px rgba(7,17,27,.1)
        padding: 0 12px
  .goods-wrapper
    flex: 1
</style>
