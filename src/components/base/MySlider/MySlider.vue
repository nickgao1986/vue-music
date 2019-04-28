<!-- better-scroll 轮播图组件 -->

<template>
  <div class="my-slider" ref="slider">
    <div class="slider-group" ref="sliderGroup">
      <slot></slot>
    </div>
    <!-- 轮播点 -->
    <div class="dots">
      <span v-for="(dot, index) in dots" :class="{ active: currentDotsIndex === index }" class="dot"></span>
    </div>
  </div>
</template>

<script>
export default{
}
</script>

<style lang="scss" scoped>
@import '~@/common/scss/const.scss';
@import '~@/common/scss/mymixin.scss';
</style>
