<template>
  <div class="Goods">
    <!-- 左边菜单 -->
    <div class="menu-wrapper" ref="menuWrapper">
      <ul class="menu-nav">
        <li class="menu-item" v-for="item of goods" :key="item.index">
          <span class="text">
            <span class="icon" :class="iconType[item.type]" v-show="item.type > 0"></span>{{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <!-- 右边商品区 -->
    <div class="goods-wrapper" ref="goodsWrapper">
      <ul class="goodsContainer">
        <li class="containerItems" v-for="item of goods" :key="item.index">
          <h1 class="categoryTitle">{{item.name}}</h1>
          <ul class="goodsCentent">
            <li class="goodsItems" v-for="items of item.foods" :key="items.index">
              <div class="goodsInfo">
                <img :src="items.image" alt="" class="goodsImg">
                <div class="goodsRight">
                  <h2 class="goodsName">{{items.name}}</h2>
                  <p class="goodsDesc">{{items.description}}</p>
                  <p class="sales-praise">
                    <span class="salesVolume">月售{{items.sellCount}}份</span>
                    <span class="praise">好评率{{items.rating}}%</span>
                  </p>
                  <p class="goodsPrice">
                    ￥<span class="price">{{items.price}}</span>
                    <span class="oldPrice" v-if="items.oldPrice">￥{{items.oldPrice}}</span>
                  </p>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import BScroll from 'better-scroll'
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
    this.requestData()
    // 图标
    this.iconType = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    // 初始化DOM元素
    this.scroll = new BScroll(this.$refs.menuWrapper)
    this.scroll = new BScroll(this.$refs.goodsWrapper)
  },
  methods: {
    // 请求商品数据
    requestData () {
      axios.get('/api/goods').then((res) => {
        const data = res.data
        if (data.errno === ERR_OK) {
          this.goods = data.data
          console.log(this.goods)
        }
      })
    }
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
        padding: 0 12px
        width: 100%
        box-sizing: border-box
        .text
          display: table-cell
          vertical-align: middle
          color: rgb(7,17,27)
          border-1px(rgba(7,17,27,.1))
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
    overflow: hidden
    .goodsContainer
      .containerItems
        .categoryTitle
          border-left: solid 2px #d9dde1
          padding-left: 12px
          height: 26px
          font-size: 12px
          color: rgb(147,153,159)
          line-height: 26px
          background: #f3f5f7
        .goodsCentent
          .goodsItems
            font-size: 12px
            border-1px(rgba(7,17,27,.1))
            &:last-child
              border-none()
            .goodsInfo
              padding: 18px
              overflow: hidden
              .goodsImg
                width: 64px
                height: 64px
                border-radius: 2px
                float: left
                margin-right: 10px
            .goodsRight
              float: left
              padding-top: 2px
              .goodsName
                font-size: 14px
                color: rgb(7,17,27)
                line-height: 14px
                margin-bottom: 8px
              .goodsDesc
                font-size: 10px
                color: rgb(147,153,159)
                line-height: 10px
                margin-bottom: 8px
              .sales-praise
                font-size: 10px
                color: rgb(147,153,159)
                line-height: 10px
                .salesVolume
                  margin-right: 12px
              .goodsPrice
                margin-top: 8px
                font-size: 10px
                font-weight: normal
                color: rgb(240,20,20)
                .price
                  font-size: 14px
                  font-weight: 700
                .oldPrice
                  color: rgb(147,153,159)
                  text-decoration: line-through
</style>
