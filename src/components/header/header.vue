<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img :src="seller.avatar" alt="" width="64" height="64">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div class="support-count" @click="showdetail()">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showdetail()">
      <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <transition name="fade">
      <div class="detail" v-show="detailShow">
        <div class="detail-wrapper clearfix">
          <div class="detail-main">
            <p>{{seller.bulletin}}</p>
          </div>
        </div>
        <div class="detail-close" @click="deletedetail()">
          <i class="icon-close"></i>
        </div>
      </div>
    </transition>
  </div>
</template>
<script>
export default {
  name: 'header',
  props:{
    seller:{
      type: Object
    }
  },
  created (){
    this.classMap = ['decrease','discount','special','invoice','guarantee'];
  },
  data () {
    return {
      detailShow:false
    }
  },
  methods:{
    showdetail(){
      this.detailShow=true;
    },
    deletedetail(){
      this.detailShow=false;
    }
  }
}
</script>
<style lang="stylus">
  @import "../../common/stylus/mixin"
  .header
    color:#fff
    position relative
    background-color rgba(7,17,27,0.5)
    .content-wrapper
      position relative
      padding :24px 12px 18px 24px
      font-size :0
      .avatar
        display:inline-block
        margin-right :16px
        vertical-align top
        img
          border-radius 2px
      .content
        display:inline-block
        font-size:14px
        .title
          margin :2px 0 8px 0
          .brand
            display :inline-block
            vertical-align top
            width:30px
            height:18px
            bg-image('brand')
            background-size:30px 18px
            background-repeat :no-repeat
          .name
            margin-left:6px
            font-size :16px
            color:rgb(255,255,255)
            font-weight bold
            line-height 18px
        .description
          font-size 12px
          color:rgb(255,255,255)
          line-height 12px
          margin-bottom 10px
        .support
          margin-bottom 2px
          .icon
            width 12px
            height 12px
            margin-right 4px
            background-size 12px 12px
            background-repeat no-repeat
            display:inline-block
            vertical-align bottom
            &.decrease
              bg-image('decrease_1')
            &.discount
              bg-image('discount_1')
            &.guarantee
              bg-image('guarantee_1')
            &.invoice
              bg-image('invoice_1')
            &.special
              bg-image('special_1')
          .text
            line-height 12px
            font-size 10px
      .support-count
        position absolute
        right 12px
        bottom 18px
        padding 0 8px
        height 24px
        line-height 24px
        border-radius 14px
        background rgba(0,0,0,0.2)
        text-align center
        .count
          vertical-align top
          font-size 10px
          line-height 24px
        .icon-keyboard_arrow_right
          font-size 10px
          line-height 24px
          margin-left 2px
    .bulletin-wrapper
      position relative
      overflow hidden
      background-color rgba(7,17,27,0.2)
      height 28px
      line-height 28px
      padding 0 12px 0 12px
      white-space nowrap
      overflow hidden
      text-overflow ellipsis
      .bulletin-title
        display inline-block
        vertical-align top
        margin-top 8px
        width 22px
        height 12px
        bg-image('bulletin')
        background-size 22px 12px
        background-repeat no-repeat
      .bulletin-text
        vertical-align top
        font-size 10px
        margin 0 4px
      .icon-keyboard_arrow_right
        position absolute
        font-size 10px
        right 12px
        top 8px

    .background
      position absolute
      left 0
      top 0
      width 100%
      height 100%
      z-index -1
      filter blur(10px)
    .fade-enter-active, .fade-leave-active {
      transition: all .8s
      opacity 1
      background rgba(7,17,27,0.8)
    }
    .fade-enter, .fade-leave-to /* .fade-leave-active in below version 2.1.8 */ {
      opacity: 0
      background rgba(7,17,27,0)
    }
    .detail
      position fixed
      top 0
      left 0
      z-index 100
      width 100%
      height 100%
      overflow auto
      background rgba(7,17,27,0.8)
      // filter: blur(5px)
      // backdrop-filter:blue(5px)
      .detail-wrapper
        min-height 100%
        .detail-main
          margin-top 64px
          padding-bottom 64px
          // border 1px solid red
      .detail-close
        position relative
        width 32px
        height 32px
        margin -64px auto 0 auto
        font-size 32px
        clear both
</style>

