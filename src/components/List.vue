<template>
  <div
    ref="listItem"
    class="listItem"
    @touchstart="touchstart()"
    @touchend="touchend()"
    @click="clickList"
  >
    <div class="listHead">
      <component v-if="icon && !slotIcon" :is="icon" />
      <slot name="icon" />
    </div>
    <div class="listBody">
      <div class="listTitle" v-if="title || slotTitle">
        <div v-if="title && !slotTitle">{{title}}</div>
        <slot name="title" />
      </div>
      <div class="listDesc" v-if="desc || slotDesc">
        <div v-if="desc && !slotDesc">{{desc}}</div>
        <slot name="desc" />
      </div>
    </div>
    <div class="listFoot">
      <div v-if="foot || slotFoot" class="footText">
        <span v-if="foot && !slotFoot">{{foot}}</span>
        <slot name="foot" />
      </div>
      <component class="footArrow" :is="ArrowRight" />
    </div>
  </div>
  <div v-if="showBorder" :class="`listBorder ${icon || slotIcon?'':'listBorderNoIcon'}`"></div>
</template>
<script lang='ts' setup>
import { ref, useSlots } from 'vue'
import { ArrowRight } from '@element-plus/icons-vue'
const slotTitle = !!useSlots().title
const slotDesc = !!useSlots().desc
const slotFoot = !!useSlots().foot
const slotIcon = !!useSlots().icon
const listItem = ref(null)
const props = defineProps({
  title: {
    type: String,
    default: ''
  },
  desc: {
    type: String,
    default: ''
  },
  foot: {
    type: String,
    default: ''
  },
  isLink: {
    type: Boolean,
    default: true
  },
  icon: {
    type: Object
  },
  showBorder: {
    type: Boolean,
    default: true
  },
  fun: {
    type: Function
  }
})
const touchstart = () => {
  ;(props.isLink || props.fun) && listItem.value.classList.add('itemTouch')
}
const touchend = () => {
  listItem.value.classList.remove('itemTouch')
}
const clickList = () => {
  props.fun && !props.disabled && props.fun()
}
</script>
<style lang='sass' scoped>
.listItem
  background-color: #ffffff
  display: flex
  align-content: stretch
  padding: 15px 10px 15px 15px
  .listHead
    padding: 2px 10px 0 0
    .icon
      opacity: 0.5
      width: 20px!important
      height: 20px!important
  .listBody
    flex: 1
    .listTitle
      font-size: 18px
    .listDesc
      font-size: 14px
      opacity: 0.5
  .listFoot
    display: flex
    align-items: center
    .footText
      font-size: 14px
      opacity: 0.5
    .footArrow
      width: 20px
      height: 20px
      opacity: 0.2
.itemTouch
  background-color: #f9f9f9
.listItem:active
  background-color: #f9f9f9
.listBorder
  height: 0px
  border-top: 1px solid #dddddd
  transform: scaleY(.5)
  margin-left: 45px
.listBorderNoIcon
  margin-left: 15px
</style>
