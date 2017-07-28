<template>
  <div class="slider" ref="slider" @touchstart="_onTouchStart" @mousedown="_onTouchStart">

    <div class="slider-wrap" ref="sliderWrap" :style="{'transform': 'translate3d(' + translateX + 'px, 0, 0)','transition-duration': transitionDuration + 'ms'}">
      <slot></slot>
    </div>
    <div class="slider-pagination">
      <span class="item" :class="{'active':index+1===currentIndex}" v-for="(item,index) in sliderItems" :key="index" @click="slide(index)"></span>
    </div>
  </div>
</template>
<script type="text/ecmascript-6">
import { addClass } from '../common/js/dom'

export default {
  props: {
    loop: {
      type: Boolean,
      default: true
    },
    autoPlay: {
      type: Boolean,
      default: true
    },
    interval: {
      type: Number,
      default: 4000
    },
    speed: {
      type: Number,
      default: 500
    }
  },
  data() {
    return {
      currentIndex: 0,
      translateX: 0,
      transitionDuration: 0,
      startPos: null,
      sliderItems: [],
      sliderWidth: 0,
      startTranslate: 0,
      delta: 0
    }
  },
  components: {

  },
  mounted() {
    setTimeout(() => {
      this._initSlider()
    }, 20)
  },
  methods: {
    _initSlider() {
      let sliderWrap = this.$refs.sliderWrap
      this.sliderItems = [].map.call(sliderWrap.children, el => el)
      let width = 0
      this.sliderWidth = this.$refs.slider.clientWidth
      for (let i = 0; i < this.sliderItems.length; i++) {
        let child = this.sliderItems[i]
        addClass(child, 'slider-item')
        child.style.width = this.sliderWidth + 'px'
        width += this.sliderWidth
      }

      if (this.loop) {
        let duplicateFirstChild = sliderWrap.firstElementChild.cloneNode(true)
        let duplicateLastChild = sliderWrap.lastElementChild.cloneNode(true)
        sliderWrap.insertBefore(duplicateLastChild, sliderWrap.firstElementChild)
        sliderWrap.appendChild(duplicateFirstChild)
        width += 2 * this.sliderWidth
        this.currentIndex = 1
        this.slide(this.currentIndex, true)
      }

      sliderWrap.style.width = width + 'px'
    },
    _onTouchStart(e) {
      this.startPos = this._getTouchPos(e)
      this.startTime = new Date().getTime()
      this.transitionDuration = 0
      this.startTranslate = this._getTranslateOffSet(this.currentIndex)
      document.addEventListener('touchmove', this._onTouchMove)
      document.addEventListener('touchend', this._onTouchEnd)
      document.addEventListener('mousemove', this._onTouchMove)
      document.addEventListener('mouseup', this._onTouchEnd)
      e.preventDefault()
    },
    _onTouchMove(e) {
      this.delta = this._getTouchPos(e) - this.startPos
      this.translateX = this.startTranslate + this.delta
      e.preventDefault()
    },
    _onTouchEnd(e) {
      this.transitionDuration = this.speed
      let isAbnormalSlide = new Date().getTime() - this.startTime < 1000
      if (this.delta < -100 || (isAbnormalSlide && this.delta < -15)) {
        this.next()
      } else if (this.delta > 100 || (isAbnormalSlide && this.delta > 15)) {
        this.prev()
      } else {
        this._revert()
      }
      document.removeEventListener('touchmove', this._onTouchMove)
      document.removeEventListener('touchend', this._onTouchEnd)
      document.removeEventListener('mousemove', this._onTouchMove)
      document.removeEventListener('mouseup', this._onTouchEnd)
    },
    _getTouchPos(e) {
      return e.changedTouches ? e.changedTouches[0].pageX : e.pageX
    },
    _getTranslateOffSet(index) {
      return -1 * index * this.sliderWidth
    },
    _revert() {
      this.slide(this.currentIndex)
    },
    slide(index, noAnimation) {
      if (this.loop) {
        if (index === this.sliderItems.length + 1) {
          this.currentIndex = 1
        } else if (index === 0) {
          this.currentIndex = this.sliderItems.length
        } else {
          this.currentIndex = index
        }
      } else {
        this.currentIndex = index
      }

      if (noAnimation) { this.transitionDuration = 0 }
      this.translateX = this._getTranslateOffSet(index)
    },
    prev() {
      let index = this.currentIndex
      this.slide(index - 1)
    },
    next() {
      let index = this.currentIndex
      this.slide(index + 1)
    }
  }

}
</script>
<style lang="stylus" scoped>
  @import "../common/stylus/variable"
  .slider
    min-height:1px
    .slider-wrap
      position:relative
      overflow:hidden
      white-space:nowrap
      .slider-item
        float:left
        box-sizing:border-box
        overflow:hidden
        text-align:center
        a
          display:block
          width:100%
          overflow:hidden
          text-decoration:none
        img
          display:block
          width:100%
    .slider-pagination
      position:absolute
      right:0
      left:0
      bottom:12px
      text-align:center
      font-size:0
      .item
        display:inline-block
        margin:0 4px
        width:8px
        height:8px
        border-radius:50%
        background:$color-text-l
        &.active
          width:20px
          border-radius:5px
          background:$color-text-ll

</style>

