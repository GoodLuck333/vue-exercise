<template>
  <div class="detailTitle">
    <div class="line"></div>
    <div class="text">{{title}}</div>
    <div class="line"></div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
      props: {
          title: {
              type: String
          }
      }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .detailTitle
    display: flex
    width: 80%
    margin: 28px auto 24px auto;
    .line
      flex: 1
      position: relative
      top: -11px
      border-bottom: 1px solid rgba(255, 255, 255, 0.2)
    .text
      padding: 4px 12px
      font-size: 14px
      font-weight: 700
      border-radius: 14px
      position: relative
      border: 1px solid rgba(255, 255, 255, 0.2)
</style>
