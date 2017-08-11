<template>
  <div class="catcontrol">
    <transition name="move">
      <div class="cart-decrease" v-show="food.count>0" @click.stop.prevent="decreaseCart">
        <span class="inner icon-remove_circle_outline"></span>
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click.stop.prevent="addCart"></div>

  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      food: {
        type: Object
      }
    },
    created() {
    },
    methods: {
      addCart(event) {
        if (!event._constructed) { // 如果是浏览器原生的话event._constructed返回folse，则阻止；如果是bscroll拆件点击事件则放行，防止pc端出现两次点击
          return;
        }
        if (!this.food.count) {
          this.$root.eventHub.$set(this.food, 'count', 1);// food中没有count属性，需要这样进行绑定才可以。此组件中的值同样会影响父组件中的值。
        } else {
          this.food.count++;
        }
        this.$root.eventHub.$emit('cart.add', event.target);
      },
      decreaseCart(event) {
        if (!event._constructed) { // 如果是浏览器原生的话event._constructed返回folse，则阻止；如果是bscroll拆件点击事件则放行，防止pc端出现两次点击
          return;
        }
        if (this.food.count) {
          this.food.count--;
        }
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .catcontrol
    font-size: 0
    .cart-decrease
      display: inline-block
      padding: 6px
      transition: all 0.4s linear
      .inner
        line-height: 24px
        font-size: 24px
        color: rgb(0, 160, 220)
        transition: all 0.4s linear
      &.move-enter-active, &.move-leave-active
        transform: translate3d(0, 0, 0)
        .inner
          display: inline-block
          transform: rotate(0)
      &.move-enter, &.move-leave-to
        opacity: 0
        transform: translate3d(24px, 0, 0)
        .inner
          transform: rotate(180deg)
    .cart-count
      display: inline-block
      vertical-align: top
      width: 12px
      padding-top: 6px
      line-height: 24px
      text-align: center
      font-size: 10px
      color: rgb(147, 153, 159)
    .cart-add
      display: inline-block
      vertical-align: top
      line-height: 24px
      font-size: 24px
      padding: 6px
      color: rgb(0, 160, 220)
</style>
