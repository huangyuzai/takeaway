<template>
  <div class="AppHeader">
    <!-- 商品信息 -->
    <div class="headerContent">
      <div class="avatar">
        <img :src="seller.avatar" alt="">
      </div>
      <div class="storeInfo">
        <div class="storeTitle">
          <span class="storeIcon"></span>
          <h1>{{seller.name}}</h1>
        </div>
        <p class="Distribution">
          {{seller.description}}/{{seller.deliveryTime}}分钟后送达
        </p>
        <div class="offer" v-if="seller.supports">
          <span class="offIcon" :class="iconType[seller.supports[0].type]"></span>
          <span class="supports">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div class="descNum" @click="showDetailBtn">
        <span class="Num" v-if="seller.supports">{{seller.supports.length}}个<span class="icon-keyboard_arrow_right" style='margin-left: 2px;'></span></span>
      </div>
    </div>
    <!-- 公告 -->
    <div class="bulletin">
      <span class='bulletinIcon'></span>
      <p class="bulletinDesc">{{seller.bulletin}}</p>
      <span class="icon-keyboard_arrow_right" style='font-size: 10px; color: rgb(255,255,255)'></span>
    </div>
    <!-- 背景图片 -->
    <div class="backgroundImg">
      <img :src="seller.avatar" alt="" width="100%" >
    </div>
    <!-- 商品详情弹出框 -->
    <div class="sellerDetail" v-show="showDetail">
      <div class="detailContainer clearfix">
        <div class="detailMain">
          <h1 class="detailTitle">{{seller.name}}</h1>
          <div class="starWrapper">
            <star :size="48" :score="seller.score"></star>
          </div>
          <div class="discountTitle">
            <span></span>
            <h2>优惠信息</h2>
            <span></span>
          </div>
          <div class="discountInfo">
            <ul>
              <li v-for="item of seller.supports" :key='item.index' v-if="seller.supports">
                <span class="discountIcon" :class="iconType[item.type]"></span>
                <span class="discountDesc">{{item.description}}</span>
              </li>
            </ul>
          </div>
          <div class="discountTitle">
            <span></span>
            <h2>商家公告</h2>
            <span></span>
          </div>
          <p class="announcement">{{seller.bulletin}}</p>
        </div>
      </div>
      <div class="detailClose" @click="hideDetailBtn">
        <i class="icon-close"></i>
      </div>
      <div class="detailBg"></div>
    </div>
  </div>
</template>

<script>
import star from 'components/star/star'
export default {
  name: 'AppHeader',
  props: {
    seller: Object
  },
  components: {
    star
  },
  data () {
    return {
      showDetail: false
    }
  },
  methods: {
    // 显示商店详情
    showDetailBtn () {
      this.showDetail = true
    },
    // 隐藏商店详情
    hideDetailBtn () {
      this.showDetail = false
    }
  },
  created () {
    this.iconType = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  }
}
</script>

<style lang="stylus" scoped>
@import '../../common/stylus/mlxin.styl'
@import '../../common/stylus/main.styl'
  .AppHeader
    background-size: 100% !important
    position: relative
    overflow: hidden
    background-color: rgba(7,17,27,.5)
    .headerContent
      padding: 0 12px
      overflow: hidden
      padding-bottom: 18px
      padding-top: 24px
      position: relative
      .avatar
        width: 64px
        height: 64px
        border-radius: 2px
        overflow: hidden
        display: inline-block
        float: left
        margin: 0px 18px 0 12px
        img
          width: 100%
          height: 100%
      .storeInfo
        float: left
        padding: 2px 0
        .storeTitle
          margin-bottom: 8px
          overflow: hidden
          .storeIcon
            width: 30px
            height: 18px
            float: left
            margin-right: 6px
            background-color: #ddd
            bg-image('../../../static/image/brand')
            background-size: 30px 18px
          h1
            font-size: 16px
            color: rgb(255,255,255)
            line-height: 18px
            font-weight: bold
            float: left
        .Distribution
          font-size: 12px
          color: rgb(255,255,255)
          font-weight: 200
          line-height: 12px
          margin-bottom: 10px
        & .supports
          font-size: 10px
          color: rgb(255,255,255)
          font-weight: 200
          line-height: 12px
        & .offer
          overflow: hidden
          .offIcon
            float: left
            margin-right: 4px
            width: 12px
            height: 12px
            background-color: #ddd
            background-size: 12px
            background-repeat: no-repeat
            &.decrease
              bg-image('../../../static/image/decrease_1')
            &.discount
              bg-image('../../../static/image/discount_1')
            &.special
              bg-image('../../../static/image/special_1')
            &.invoice
              bg-image('../../../static/image/invoice_1')
            &.guarantee
              bg-image('../../../static/image/guarantee_1')
          .supports
            float: left
            line-height: 12px
      .descNum
        position: absolute
        bottom: 15px
        right: 12px
        background: rgba(0,0,0,.2)
        border-radius: 15px
        color: rgb(255,255,255)
        font-size: 10px
        font-weight: 200
        line-height: 12px
        height: 24px
        box-sizing: border-box
        padding: 7px 8px
        vertical-align: top
    .bulletin
      height: 28px
      padding: 0 12px
      overflow: hidden
      background: rgba(7,17,27,.2)
      line-height: 28px
      font-size: 0
      display: flex
      align-items: center
      .bulletinIcon
        bg-image('../../../static/image/bulletin')
        background-size: 22px 12px
        background-repeat: no-repeat
        display: inline-block
        width: 22px
        height: 12px
        margin-right: 4px
      .bulletinDesc
        display: inline-block
        font-size: 10px
        color: rgb(255,255,255)
        font-weight: 200
        width: 315px
        margin-right: 4px
        ellipsis()
    .backgroundImg
      position: absolute
      top: 0
      left: 0
      width: 100%
      height: 100%
      z-index: -1
      filter: blur(10px)
    .sellerDetail
      width: 100%
      height: 100%
      background: rgba(7,17,27,.8)
      position: fixed
      top: 0
      left: 0
      z-index: 9
      overflow: auto
      .detailContainer
        width: 100%
        min-height: 100%
        .detailMain
          margin-top: 64px
          padding-bottom: 64px
          .detailTitle
            font-size: 16px
            font-weight: 700
            color: rgb(255,255,255)
            line-height: 16px
            text-align: center
            margin-bottom: 16px
          .starWrapper
            text-align: center
            padding: 2px 0
            margin-bottom: 28px
          .discountTitle
            font-size: 16px
            color: #ffffff
            text-align: center
            font-weight: 700
            padding: 0 36px
            display: flex
            align-items: center
            justify-content: center
            margin-bottom: 24px
            h2
              padding: 0 12px
            span
              display: block
              height: 2px
              flex: 1
              background: rgba(255,255,255,.2)
          .discountInfo
            padding: 0 36px
            margin-bottom: 28px
            ul
              padding: 0 12px
              color: rgb(255,255,255)
              li
                overflow: hidden
                margin-bottom: 12px
                line-height: 12px
                .discountIcon
                  display: inline-block
                  height: 16px
                  width: 16px
                  margin-right: 6px
                  float: left
                  background-color: #ddd
                  background-size: 16px
                  background-repeat: no-repeat
                .discountDesc
                  font-size: 12px
                  font-weight: 200
                .decrease
                  bg-image('../../../static/image/decrease_1')
                .discount
                  bg-image('../../../static/image/discount_1')
                .special
                  bg-image('../../../static/image/special_1')
                .invoice
                  bg-image('../../../static/image/invoice_1')
                .guarantee
                  bg-image('../../../static/image/guarantee_1')
          .announcement
            padding: 0 48px
            font-size: 12px
            font-weight: 200
            color: #fff
            line-height: 24px
      .detailClose
        position: relative
        width: 32px
        height: 32px
        margin: -64px auto 0 auto
        clear: both
        font-size: 32px
        color: rgba(255,255,255,.5)
      .detailBg
        width: 100%
        height: 100%
        position: absolute
        top: 0
        left: 0
        background: rgba(7,17,27,.8)
        filter: blur(10px)
        z-index: -1
</style>
