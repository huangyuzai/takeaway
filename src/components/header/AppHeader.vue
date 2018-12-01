<template>
  <div class="AppHeader" :style="{background: 'url('+ seller.avatar +') no-repeat'}">
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
      <div class="descNum">
        <span class="Num">5个<span class="fa fa-angle-right" style='margin-left: 4px;'></span></span>
      </div>
    </div>
    <div class="bulletin">
      <span class='bulletinIcon'></span>
      <p class="bulletinDesc">{{seller.bulletin}}</p>
      <span class="fa fa-angle-right" style='font-size: 10px; color: rgb(255,255,255)'></span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppHeader',
  props: {
    seller: Object
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

</style>
