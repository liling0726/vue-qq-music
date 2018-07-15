<template>
  <div id="app">
    <m-header />
    <router-view/>
  </div>
</template>

<script>
import MHeader from 'components/m-header'
export default {
  components: {
    MHeader
  }
}
</script>
<style lang="less">
</style>
