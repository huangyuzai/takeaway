<template>
  <div class="star" :class="starType">
    <span class="star-item" :class="item" v-for="item of star" :key="item.index"></span>
  </div>
</template>

<script>
const LENGTH = 5
const CLS_ON = 'on'
const CLS_HALF = 'half'
const CLS_OFF = 'off'
export default {
  name: 'star',
  props: {
    size: {
      type: Number
    },
    score: {
      type: Number
    }
  },
  computed: {
    //   监听传进来的 size 动态设置 star 的 class
    starType () {
      return 'star-' + this.size
    },
    // 计算星级
    star () {
      let result = []
      let score = Math.floor(this.score * 2) / 2 // 向下取整
      let hasDecimal = score % 1 !== 0 // 是否有半星
      let integer = Math.floor(score) // 全星的个数
      for (let i = 0; i < integer; i++) {
        result.push(CLS_ON) // 填充全星
      }
      if (hasDecimal) {
        result.push(CLS_HALF) // 如果有半星则填充半星
      }
      while (result.length < LENGTH) {
        result.push(CLS_OFF) // 如果星级不满5星，则后面的星级填充为空星
      }
      return result
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '../../common/stylus/mlxin.styl'
  .star
    font-size: 0
    .star-item
      display: inline-block
    &.star-48
      .star-item
        width: 20px
        height: 20px
        margin-right: 22px
        background-size: 20px 20px
        &:last-child
          margin-right: 0
        &.on
          bg-image('../../../static/image/star48_on')
        &.half
          bg-image('../../../static/image/star48_half')
        &.off
          bg-image('../../../static/image/star48_off')
    &.star-36
      .star-item
        width: 15px
        height: 15px
        margin-right: 6px
        background-size: 15px 15px
        &:last-child
          margin-right: 0
        &.on
          bg-image('../../../static/image/star36_on')
        &.half
          bg-image('../../../static/image/star36_half')
        &.off
          bg-image('../../../static/image/star36_off')
    &.star-24
      .star-item
        width: 10px
        height: 10px
        margin-right: 3px
        background-size: 10px 10px
        &:last-child
          margin-right: 0
        &.on
          bg-image('../../../static/image/star24_on')
        &.half
          bg-image('../../../static/image/star24_half')
        &.off
          bg-image('../../../static/image/star24_off')

</style>
