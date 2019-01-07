<template>
    <div class="star" :class="starType">
        <span v-for="(item,index) in itemClasses" :class="item"
        class="star-item" :key="index"
        ></span>
    </div>
</template>

<script>
const LENGTH = 5
const CLS_ON = 'on'
const CLS_HALF = 'half'
const CLS_OFF = 'off'

export default {
  props: {
    size: {
      type: Number
    },
    score: {
      type: Number
    }
  },
  computed: {
    starType () {
      return 'star-' + this.size
    },
    itemClasses () {
      let result = []
      console.log('0---', this.score)
      let score = Math.floor(this.score * 2) / 2 // 要么是整数，要么是xxx.5
      console.log('1-------', score)
      let hasDecimal = score % 1 !== 0
      let integer = Math.floor(score)
      console.log('integer', score)
      for (let i = 0; i < integer; i++) {
        result.push(CLS_ON)
        console.log(i)
      }
      if (hasDecimal) {
        result.push(CLS_HALF)
      }
      while (result.length < LENGTH) {
        result.push(CLS_OFF)
      }
      return result
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '~@/common/stylus/mixin.styl'
    .star
        .star-item
            display inline-block
            background-repeat no-repeat
            &:last-child
                margin-right 0
        &.star-48
            .star-item
                width 20px
                height 20px
                margin-right 22px
                background-size 20px 20px
                &.on
                    bg-image('star48_on')
                &.half
                    bg-image('star48_half')
                &.off
                    bg-image('star48_off')
        &.star-36
            .star-item
                width 15px
                height 15px
                margin-right 16px
                background-size 15px 15px
                &.on
                    bg-image('star36_on')
                &.half
                    bg-image('star36_half')
                &.off
                    bg-image('star36_off')
        &.star-24
            .star-item
                width 10px
                height 10px
                margin-right 3px
                background-size 10px 10px
                &.on
                    bg-image('star24_on')
                &.half
                    bg-image('star24_half')
                &.off
                    bg-image('star24_off')
</style>
