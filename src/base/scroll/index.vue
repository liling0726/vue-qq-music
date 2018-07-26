<template>
  <div ref="wrapper">
    <slot> </slot>
  </div>
</template>
<script>
import BScroll from 'better-scroll'
const DIRECTION_V = 'vertical'
const DIRECTION_H = 'horizontal'
export default {
  props: {
    // 是否可以下拉刷新
    pullup: {
      type: Boolean,
      default: false
    },
    // 滚动数据
    data: {
      type: Array,
      default: null
    },
    // 刷新延迟时间
    refreshDelay: {
      type: Number,
      default: 20
    },
    // 滚动方向
    direction: {
      type: String,
      default: DIRECTION_V
    },
    // 是否可点击
    click: {
      type: Boolean,
      default: false
    },
    // 滚动事件派发的时机，可选值 1，2，3 默认 0
    probeType: {
      type: Number,
      default: 0
    },
    // 是否监听滚动
    listenScroll: {
      type: Boolean,
      default: false
    }
  },
  watch: {
    data() {
      setTimeout(() => {
        this.refresh()
      }, this.refreshDelay)
    }
  },
  mounted() {
    // 添加延迟，保证DOM已经渲染完成
    setTimeout(() => {
      this._initScroll()
    }, 20)
  },
  methods: {
    _initScroll() {
      if (!this.$refs.wrapper) return
      this.scroll = new BScroll(this.$refs.wrapper, {
        eventPassthrough: this.direction === DIRECTION_V ? DIRECTION_H : DIRECTION_V,
        click: this.click,
        probeType: this.probeType
      })
      console.log('scroll', this.listenScroll, this.probeType)
      if (this.listenScroll) {
        this.scroll.on('scroll', (pos) => {
          this.$emit('scroll', pos)
        })
      }

      if (this.pullup) {
        this.scroll.on('scrollEnd', () => {
          if (this.scroll.y <= (this.scroll.maxScrollY + 50)) {
            this.$emit('scrollToEnd')
          }
        })
      }

      if (this.beforeScroll) {
        this.scroll.on('beforeScrollStart', () => {
          this.$emit('beforeScroll')
        })
      }
    },
    refresh() {
      // 代理better-scroll的refresh方法
      this.scroll && this.scroll.refresh()
    }
  }
}
</script>
<style lang="less">
</style>
