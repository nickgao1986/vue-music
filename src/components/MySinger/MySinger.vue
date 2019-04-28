<!-- 歌手页组件 -->
<template>
  <div class="my-singer" ref="singerRef">
    singer
    <router-view></router-view>
  </div>
</template>

<script>
export default {
}
</script>

<style lang="scss" scoped>
@import '~@/common/scss/const.scss';
@import '~@/common/scss/mymixin.scss';

.my-singer {
  position: fixed;
  top: 88px;
  bottom: 0;
  width: 100%;
}
</style>
