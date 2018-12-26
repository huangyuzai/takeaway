<template>
  <div class="Goods">
    <!-- 左边菜单 -->
    <div class="menu-wrapper">
      <ul class="menu-nav">
        <li class="menu-item" v-for="item of goods" :key="item.index">
          <span class="text">
            <span class="icon" :class="iconType[item.type]" v-show="item.type > 0"></span>{{item.name}}
          </span>
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
    // 图标
    this.iconType = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  }
}
</script>

<style lang="stylus" scoped>
@import '../../common/stylus/mlxin.styl'

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
    overflow: hidden
    .menu-nav
      .menu-item
        font-size: 12px
        color: rgb(7,17,27)
        font-weight: 200
        line-height: 14px
        height: 54px
        display: table
        align-items: center
        border-bottom: solid 1px rgba(7,17,27,.1)
        padding: 0 12px
        width: 100%
        box-sizing: border-box
        .text
          display: table-cell
          vertical-align: middle;
          color: rgb(7,17,27);
          .icon
            display: inline-block
            height: 12px
            width: 12px
            margin-right: 2px
            background-color: #ddd
            background-size: 12px
            background-repeat: no-repeat
          .decrease
            bg-image('../../../static/image/decrease_3')
          .discount
            bg-image('../../../static/image/discount_3')
          .special
            bg-image('../../../static/image/special_3')
          .invoice
            bg-image('../../../static/image/invoice_3')
          .guarantee
            bg-image('../../../static/image/guarantee_3')
  .goods-wrapper
    flex: 1
</style>
