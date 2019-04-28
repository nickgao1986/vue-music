<!-- 推荐页组件 -->

<template>
  <div class="my-recommend" ref="recommendRef">
    <router-view></router-view>
  </div>
</template>

<script>
import { getRecommend } from '@/api/recommend.js'

export default {
  components: {
  },
  data () {
    return {
      recommends: [],
      lists: []
    }
  },
  created () {
    this._getRecommend()
    setTimeout(() => {
      this._getList()
    }, 1000)
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

.my-recommend {
  position: fixed;
  width: 100%;
  top: 88px;
  bottom: 0;
  .recommend-content {
    height: 100%;
    overflow: hidden;
    .slide-wrapper {
      position: relative;
      width: 100%;
      overflow: hidden;
    }
    .recommend-list {
      .list-title {
        height: 65px;
        line-height: 65px;
        text-align: center;
        font-size: $font-size-medium;
        color: $color-theme;
      }
      .item {
        display: flex;
        align-items: center;
        box-sizing: border-box;
        padding: 0 20px 20px 20px;
        .icon {
          flex: 0 0 60px;
          width: 60px;
          padding-right: 20px;
        }
        .text {
          display: flex;
          flex-direction: column;
          justify-content: center;
          flex: 1;
          line-height: 20px;
          overflow: hidden;
          font-size: $font-size-medium;
          .name {
            margin-bottom: 10px;
            color: $color-text;
          }
          .desc {
            color: $color-text-d;
          }
        }
      }
    }
    .loading-container {
      position: absolute;
      width: 100%;
      top: 50%;
      transform: translateY(-50%);
    }
  }
}
</style>
