<template>
  <div id="app">
    <m-header />
    <tab />
    <router-view/>
  </div>
</template>

<script>
import MHeader from 'components/m-header'
import Tab from 'components/tab'
export default {
  components: {
    MHeader,
    Tab
  }
}
</script>
<style lang="less">
* { touch-action: none; }
</style>
