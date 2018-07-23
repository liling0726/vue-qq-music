<template>
  <transition name="slide">
    <music-list :title="title" :bg-image="bgImage" :songs="songs"></music-list>
  </transition>
</template>
<script>
import musicList from 'components/music-list'

export default {
  components: {
    musicList
  },
  data() {
    return {
      title: '',
      songs: [],
      bgImage: ''
    }
  }
}
</script>
<style lang="less">
.slide-enter-active,
.slide-leave-active {
  transition: all 0.3s;
}
.slide-enter,
.slide-leave-to {
  transform: translate3d(100%, 0, 0);
}
</style>
