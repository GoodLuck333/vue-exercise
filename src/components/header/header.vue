<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar"/>
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
      <div v-if="seller.supports" class="support-count" @click="showDetail">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail">
      <span class="bulletin-title"></span><span
      class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%">
    </div>
    <div v-show="detailShow" class="detail" transition="fade">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
          <div class="nameStar noScroll">
            <h1 class="name">{{seller.name}}</h1>
            <div class="star-wrapper">
              <star :size="48" :score="seller.score"></star>
            </div>
          </div>
          <div class="detail-content">
            <detail-title :title="'优惠信息'"></detail-title>
            <ul v-if="seller.supports" class="supports">
              <li class="support-item" v-for="item in seller.supports">
                <span class="icon" :class="classMap[seller.supports[$index].type]"></span>
                <span class="text">{{seller.supports[$index].description}}</span>
              </li>
            </ul>
            <detail-title :title="'商家公告'"></detail-title>
            <div class="bulletin">
              <p class="content">{{seller.bulletin}}</p>
            </div>
          </div>
          <div class="bottomWrite noScroll"></div>
        </div>
      </div>
      <div class="detail-close">
        <i class="icon-close" @click="hideDetail"></i>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">

  import star from 'components/star/star';
  import detailTitle from 'components/detailTitle/detailTitle';

  export default{
    props: {
      seller: {
        type: Object
      }
    },
    data() {
      return {
        detailShow: false
      };
    },
    methods: {
      showDetail() {
        this.detailShow = true;
        document.querySelector('.detail-content').style.height = document.documentElement.clientHeight - 196 + 'px';
        document.querySelector('.noScroll').addEventListener('touchmove', function (event) {
          event.preventDefault();
          event.stopPropagation();
          document.body.scrollTop = 0;
          return false;
        }, false);
      },
      hideDetail() {
        this.detailShow = false;
      }
    },
    created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    },
    components: {
      star,
      detailTitle
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">

  @import "../../common/stylus/base.styl"
  @import "../../common/stylus/mixin.styl"

  .header
    position: relative
    overflow: hidden
    color: #fff;
    background: rgba(7, 17, 27, 0.5)
    .content-wrapper
      position: relative
      padding: 24px 12px 18px 24px
      font-size: 0
      .avatar
        display: inline-block
        vertical-align: top
        img
          border-radius: 2px
      .content
        display: inline-block
        margin-left: 16px
        .title
          margin: 2px 0 8px 0
          .brand
            display: inline-block
            vertical-align: top
            width: 30px
            height: 18px
            bg-image('brand')
            background-size: 30px 18px
            background-repeat: no-repeat
          .name
            margin-left: 6px
            font-size: 16px
            line-height: 18px
            font-weight: bold
        .description
          margin-bottom: 10px
          line-height: 12px
          font-size: 12px
        .support
          .icon
            display: inline-block
            vertical-align: top
            width: 12px
            height: 12px
            margin-right: 4px
            background-size: 12px
            background-repeat: no-repeat
            border-radius: 2px
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
            line-height: 12px
            font-size: 10px
      .support-count
        position: absolute
        right: 12px
        bottom: 16px
        padding: 0 16px 0 8px
        height: 16px
        line-height: 16px
        border-radius: 14px
        background: rgba(0, 0, 0, 0.2)
        text-align: center
        .count
          font-size: 10px
        .icon-keyboard_arrow_right
          margin-left: 2px
          line-height: 16px
          font-size: 10px
          &:before
            position: absolute
            top: 1px
            right: 6px
    .bulletin-wrapper
      position: relative
      height: 28px
      line-height: 28px
      padding: 0 22px 0 12px
      white-space: nowrap
      overflow: hidden
      text-overflow: ellipsis
      background: rgba(7, 17, 27, 0.2)
      .bulletin-title
        display: inline-block
        vertical-align: top
        margin-top: 7px
        width: 22px
        height: 12px
        bg-image('bulletin')
        background-size: 22px 12px
        background-repeat: no-repeat
      .bulletin-text
        vertical-align: top
        margin: 0 4px
        font-size: 10px
      .icon-keyboard_arrow_right
        position: absolute
        font-size: 10px
        right: 12px
        top: 8px

    .background
      position: absolute
      top: 0
      left: 0
      width: 100%
      height: 100%
      z-index: -1
      filter: blur(10px)
    .detail
      position: fixed
      z-index: 100
      top: 0
      left: 0
      width: 100%
      height: 100%
      overflow: auto
      transition: all 0.6s
      backdrop-filter: blur(10px);
      &.fade-transition
        opacity: 1
        background: rgba(7, 17, 27, 0.8)
      &.fade-enter, &.fade-leave
        opacity: 0
        background: rgba(7, 17, 27, 0.8)
      .detail-wrapper
        min-height: 100%
        width: 100%
        overflow: hidden
        .detail-main
          .nameStar
            padding-top: 64px
            .name
              line-height: 16px
              text-align: center
              font-size: 16px
              font-weight: 700
              color: rgb(255, 255, 255)
            .star-wrapper
              margin-top: 18px
              padding: 2px 0
              text-align: center
          .detail-content
            -webkit-overflow-scrolling: touch;
            overflow: auto
            .supports
              width: 80%
              margin: 0 auto
              .support-item
                padding: 0 12px
                margin-bottom: 12px
                font-size: 0
                &:last-child
                  margin-bottom: 0
                .icon
                  display: inline-block
                  width: 16px
                  height: 16px
                  vertical-align: top
                  margin-right: 6px
                  background-size: 16px
                  background-repeat: no-repeat
                  &.decrease
                    bg-image('decrease_2')
                  &.discount
                    bg-image('discount_2')
                  &.guarantee
                    bg-image('guarantee_2')
                  &.invoice
                    bg-image('invoice_2')
                  &.special
                    bg-image('special_2')
                .text
                  line-height: 16px
                  font-size: 12px
                  font-weight: 200
            .bulletin
              width: 80%
              margin: 0 auto
              .content
                padding: 0 12px
                line-height: 24px
                font-size: 12px
          .bottomWrite
            padding-bottom: 64px
      .detail-close
        position: relative
        width: 32px
        height: 32px
        margin: -64px auto 0 auto
        clear: both
        font-size: 32px
        color: rgba(255, 255, 255, 0.5)
</style>
