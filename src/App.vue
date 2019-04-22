<template>
  <div id="app">
    <div class="header">
      <v-header :seller="seller"></v-header>
    </div>
    <div class="tab">
      <div class="tab-item">
        <router-link tag="a" to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link tag="a" to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link tag="a" to="/seller">商家</router-link>
      </div>
    </div>
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script>
import header from './components/header/header.vue'
const responseNo = 0
export default {
  name: 'App',
  components:{
    'v-header':header//注册组件通常用'v-' + name来命名
  },
  data(){
    return {
      seller:{}
    }
  },
  created() {
    this.$http.get('/api/seller').then(response => {
      if(response.data.errno === responseNo){
        this.seller = response.data.seller
      }
    })
  },
}
</script>

<style lang="scss" scoped>
  @import "./common/sass/mixin.scss";
  #app{
    .tab{
      display: flex;
      width: 100%;
      height: 40px;
      line-height: 40px;
      @include border-1px( rgba(7,17,27,0.1));

      .tab-item{
        flex: 1;
        text-align: center;

        .a{
          display: block;
          font-size: 14px;
          color: rgb(77,85,93);
        }

        .active{
          color: rgb(240, 20, 20)
        }
      }
    }
  }
</style>
