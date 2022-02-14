<template>
  <div
    v-loading="disabled"
    class="listItem listItemActive"
    ref="listItem"
    @touchstart="touchstart()"
    @touchend="touchend()"
    @click="clickList"
  >
    <div class="head" v-if="icon || slotIcon">
      <component v-if="icon && !slotIcon" :is="icon" />
      <slot name="icon" />
    </div>
    <div class="body">
      <div v-if="title || slotTitle" class="listTitle">
        <span v-if="title && !slotTitle">{{title}}</span>
        <slot name="title" />
      </div>
      <div v-if="desc || slotDesc" class="listDesc">
        <span v-if="desc && !slotDesc">{{desc}}</span>
        <slot name="desc" />
      </div>
    </div>
    <div class="foot">
      <div v-if="foot || slotFoot" class="footText">
        <span v-if="foot && !slotFoot">{{foot}}</span>
        <slot name="foot" />
      </div>
      <el-icon class="arrowright" v-if="isLink">
        <arrow-right />
      </el-icon>
    </div>
  </div>
  <div v-if="showBorder" :class="`listBorder ${icon || slotIcon?'':'listBorderNoIcon'}`"></div>
</template>
<script lang='ts' setup>
import { getCurrentInstance, watch, useSlots, onMounted } from 'vue'
import { ArrowRight } from '@element-plus/icons-vue'
const slotIcon = !!useSlots().icon
const slotTitle = !!useSlots().title
const slotDesc = !!useSlots().desc
const slotFoot = !!useSlots().foot
const { proxy } = getCurrentInstance()
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
    default: false
  },
  icon: {
    type: Object
  },
  fun: {
    type: Function
  },
  showBorder: {
    type: Boolean,
    default: true
  },
  disabled: {
    type: Boolean,
    default: false
  }
})
const touchstart = () => {
  ;(props.isLink || props.fun) &&
    proxy.$refs.listItem.classList.add('itemTouch')
}
const touchend = () => {
  proxy.$refs.listItem.classList.remove('itemTouch')
}
const clickList = () => {
  props.fun && !props.disabled && props.fun()
}
onMounted(() => {
  !props.isLink &&
    !props.fun &&
    proxy.$refs.listItem.classList.remove('listItemActive')
})
</script>
<style lang='sass' scoped>
@import '../styles/element/index.scss'
.listItem
  padding: 15px
  display: flex
  background-color: $--color-white
.listBorder
  height: 0px
  border-top: 1px solid var(--el-border-color-base)
  transform: scaleY(.5)
  margin-left: 45px
.listBorderNoIcon
  margin-left: 15px
.itemTouch
  background-color: $--color-info-light-9
.listItemActive:active
  background-color: $--color-info-light-9
.head
  padding: 2px 10px 0 0
  color: $--color-primary
  .icon
    width: 20px!important
    height: 20px!important
.body
  flex: 1
  padding: 0px 5px 0 0
.foot
  display: flex
  align-items: center
  .footText
    color: $--color-info-light-5
    font-size: 14px
    margin: 0 5px
  .arrowright
    color: var(--el-border-color-base)
    font-size: 20px
.listTitle
  font-size: 18px
  color: $--color-black
.listDesc
  font-size: 14px
  color: $--color-info-light-3
</style>
