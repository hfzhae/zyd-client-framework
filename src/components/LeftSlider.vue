<template>
  <div ref="leftSliderItem" class="leftSliderItem">
    <div
      @touchstart="touchstart"
      @touchmove="touchMove"
      @touchend="touchend"
      :style="deleteSlider"
      :class="`content ${itemClass?itemClass:'contentBackgroundColor'}`"
    >
      <slot />
      <div v-if="showBorder" class="listBorder"></div>
    </div>
    <div
      ref="rightMenu"
      :class="`rightMenu ${menuClass?menuClass:'rightMenuBackgroundColor'}`"
      v-if="slotRightMenu"
    >
      <slot name="rightMenu" />
    </div>
  </div>
</template>
<script lang='ts' setup>
import { ref, shallowRef, useSlots } from 'vue'
const props = defineProps({
  menuClass: {
    type: String
  },
  showBorder: {
    type: Boolean,
    default: true
  },
  itemClass: {
    type: String
  }
})
const slotRightMenu = !!useSlots().rightMenu
const startX = shallowRef(0)
const moveX = shallowRef(0)
const endX = shallowRef(0)
const disX = shallowRef(0)
const deleteSlider = shallowRef('')
const leftSliderItem = ref(null)
const rightMenu = ref(null)
const touchstart = ev => {
  ev = ev || event
  //tounches类数组，等于1时表示此时有只有一只手指在触摸屏幕
  if (ev.touches.length == 1) {
    // 记录开始位置
    startX.value = ev.touches[0].clientX
  }
}
const touchMove = ev => {
  ev = ev || event
  //获取删除按钮的宽度，此宽度为滑块左滑的最大距离
  let wd = (rightMenu.value && rightMenu.value.offsetWidth) || 50
  if (ev.touches.length == 1) {
    // 滑动时距离浏览器左侧实时距离
    moveX.value = ev.touches[0].clientX
    //起始位置减去 实时的滑动的距离，得到手指实时偏移距离
    disX.value = startX.value - moveX.value + endX.value
    // 如果是向右滑动或者不滑动，不改变滑块的位置
    if (disX.value < 0 || disX.value == 0) {
      deleteSlider.value = 'transform:translateX(0px)'
      // 大于0，表示左滑了，此时滑块开始滑动
    } else if (disX.value > 0) {
      //具体滑动距离我取的是 手指偏移距离*5。
      deleteSlider.value = 'transform:translateX(-' + disX.value + 'px)'
      // 最大也只能等于删除按钮宽度
      if (disX.value >= wd + 50) {
        deleteSlider.value = 'transform:translateX(-' + (wd + 50) + 'px)'
      }
    }
  }
}
const touchend = ev => {
  ev = ev || event
  let wd = (rightMenu.value && rightMenu.value.offsetWidth) || 0
  if (ev.changedTouches.length == 1) {
    endX.value = ev.changedTouches[0].clientX
    disX.value = startX.value - endX.value
    //如果距离小于删除按钮一半,强行回到起点
    if (disX.value >= wd / 2) {
      //大于一半 滑动到最大值
      deleteSlider.value = 'transform:translateX(-' + wd + 'px)'
      endX.value = wd
    } else {
      deleteSlider.value = 'transform:translateX(0px)'
      endX.value = 0
    }
  }
}
</script>
<style lang='sass' scoped>
.leftSliderItem
  display: flex
  align-items: stretch
  position: relative
  user-select: none
  .content
    z-index: 100
    transition: 0.1s
    width: 100%
  .rightMenuBackgroundColor
    background: #df5327
  .rightMenu
    position: absolute
    top: 0
    right: 0
    height: 99%
    color: #fff
    text-align: center
    display: flex
    align-items: center
    justify-content: center
  .contentBackgroundColor
    background-color: #ffffff
</style>