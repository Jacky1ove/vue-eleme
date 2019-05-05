<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="cart-decrease" @click="decreaseCart" v-show="food.count>0">
        <span class="inner icon-remove_circle_outline"></span>
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click="addCart"></div>
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
    console.log(this.food);
  },
  methods: {
    addCart(event) {
      console.log(event);
      if (!this.food.count) {
        // this.food.count = 1;
        this.$set(this.food, "count", 1);
      } else {
        this.food.count++;
      }
      this.$emit('cartAdd',event.target)
    },
    decreaseCart() {
      if (this.food.count) {
        this.food.count--;
      }
    }
  }
};
</script>

<style scoped lang="scss">
@import "../../common/sass/icon.css";
.cartcontrol {
  font-size: 0;
  .cart-decrease{
    display: inline-block;
    padding: 6px;
    transition: all 0.4s linear;
    &.move-transition{
      opacity: 1;
      transform: translate3d(0,0,0)
    }
    .inner{
      display: inline-block;
      line-height: 24px;
      font-size: 24px;
      color: rgb(0, 160, 220);
      transition: all 0.4s linear;
      transform: rotate(0);
    }
    &.move-enter,&.move-leave-to{
      opacity: 0;
      transform: translate3d(24px,0,0);
      .inner{
        transform: rotate(180deg);
      }
    }
  }
  .cart-count {
    display: inline-block;
    vertical-align: top;
    width: 12px;
    padding-top: 6px;
    line-height: 24px;
    text-align: center;
    font-size: 10px;
    color: rgb(153, 147, 159);
  }
  .cart-add {
    display: inline-block;
    line-height: 24px;
    padding: 6px;
    font-size: 24px;
    color: rgb(0, 160, 220);
  }
}
</style>
