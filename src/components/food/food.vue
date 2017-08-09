<template>
  <transition name="move">
    <div class="food" v-show="showFlag" @click="hidden">dhfehdfe</div>
  </transition>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      food: {
        type: Object
      }
    },
    data() {
      return {
        showFlag: false
      };
    },
    methods: {
      show() {
        this.showFlag = true;
      },
      hidden() {
        this.showFlag = false;
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .food
    position: fixed
    left: 0
    top: 0
    bottom: 48px
    z-index: 30
    width: 100%
    background: #fff
    transition: all 0.2s
    &.move-entry-active, &.move-leave-active
      transform: translate3d(0, 0, 0)
    &.move-entry, &.move-leave-to
      transform: translate3d(100%, 0, 0)
</style>
