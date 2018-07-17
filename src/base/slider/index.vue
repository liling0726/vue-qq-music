<template>
  <div ref="wrapper">
    <slot> </slot>
  </div>
</template>
<script>
import BScroll from 'better-scroll'
export default {
  props: {
    data: {
      type: Array
    }
  },
  mounted() {
    // 添加延迟，保证DOM已经渲染完成
    this.$nextTick(() => {
      this.scroll = new BScroll(this.$refs.wrapper)
    })
  }
}
</script>
<style lang="less">
</style>
