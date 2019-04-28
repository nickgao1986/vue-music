<!-- 推荐页组件 -->

<template>
  <div class="my-recommend" ref="recommendRef">
    <router-view></router-view>
      <!-- 轮播图，当请求到 recommends 时才渲染 -->
      <div v-if="recommends.length" class="slide-wrapper">
        <my-slider>
          <div v-for="recommend in recommends">
            <a :href="recommend.linkUrl">
              <img @load="loadImg" :src="recommend.picUrl" class="needsclick">
            </a>
          </div>
        </my-slider>
      </div>
  </div>
</template>

<script>
import { getRecommend } from '@/api/recommend.js'
import MySlider from '@/components/base/MySlider/MySlider'
export default {
  components: {
    MySlider
  },
  data () {
    return {
      recommends: [],
      lists: []
    }
  },
  created () {
    this._getRecommend()
  },
  methods: {
    // 获取轮播图数据
    _getRecommend () {
      getRecommend().then((res) => {
        if (res.code === 0) {
          // console.log(res)
          this.recommends = res.data.slider
        }
      })
    },
    // 当首次获取到图片时，Better-scroll 重新计算
    loadImg () {
      if (!this.flag) {
        this.$refs.scroll.refresh()
        this.flag = true
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~@/common/scss/const.scss';
@import '~@/common/scss/mymixin.scss';

</style>
