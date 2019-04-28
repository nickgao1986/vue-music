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
import BScroll from 'better-scroll'
import { myDOM } from '@/common/js/myutils.js'
export default{
  components: {},
  data () {
    return {
      dots: [],
      currentDotsIndex: 0
    }
  },
  props: {
    // 是否循环播放
    loop: {
      type: Boolean,
      default: true
    },
    // 是否自动播放
    autoPlay: {
      type: Boolean,
      default: true
    },
    // 轮播延时
    delay: {
      type: Number,
      default: 3000
    }
  },
  created () {},
  mounted() {
    setTimeout(() => {
      this._setSliderWidth()
      this._initSlider()
    }, 20)
  },
  methods: {
    _setSliderWidth (isResize) {
      // 拿到传过来的图片
      this.children = this.$refs.sliderGroup.children
      // console.log(this.children) // (5) [div, div, div, div, div]

      // 拿到父元素（slider）宽度
      let width = 0
      let sliderWidth = this.$refs.slider.clientWidth

      // 动态添加 class、width
      for (let i = 0; i < this.children.length; i++) {
        let child = this.children[i]
        myDOM.addClass(child, 'slider-item')

        child.style.width = sliderWidth + 'px'
        width += sliderWidth
      }

      if (this.loop && !isResize) {
        width += 2 * sliderWidth
      }

      this.$refs.sliderGroup.style.width = width + 'px'
    },
    // 初始化轮播图
    _initSlider () {
      this.slider = new BScroll(this.$refs.slider, {
        scrollX: true,
        scrollY: false,
        momentum: false,
        snap: true,
        snapLoop: this.loop,
        snapThreshold: 0.3,
        snapSpeed: 400
      })
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~@/common/scss/const.scss';
@import '~@/common/scss/mymixin.scss';

.my-slider {
  min-height: 1px;
  .slider-group {
    position: relative;
    overflow: hidden;
    white-space: nowrap;
    .slider-item {
      float: left;
      box-sizing: border-box;
      overflow: hidden;
      text-align: center;
      a {
        display: block;
        width: 100%;
        overflow: hidden;
        text-decoration: none;
      }
      img {
        display: block;
        width: 100%
      }
    }
  }
}
</style>
