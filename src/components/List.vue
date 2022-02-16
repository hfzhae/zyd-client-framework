<template>
  <div
    ref="listItem"
    :class="`listItem listItemActive ${itemClass?itemClass:'listItemBackgroundColor'}`"
    @touchstart="touchstart()"
    @touchend="touchend()"
    @click="clickList"
  >
    <div v-if="disabled" class="maks" @click.stop="()=>{}"></div>
    <div class="listHead">
      <component :class="iconClass?iconClass:''" v-if="icon && !slotIcon" :is="icon" />
      <slot name="icon" />
    </div>
    <div class="listBody">
      <div :class="`listTitle ${titleClass?titleClass:''}`" v-if="title || slotTitle">
        <div v-if="title && !slotTitle">{{title}}</div>
        <slot name="title" />
      </div>
      <div :class="`listDesc ${descClass?descClass:''}`" v-if="desc || slotDesc">
        <div v-if="desc && !slotDesc">{{desc}}</div>
        <slot name="desc" />
      </div>
    </div>
    <div class="listFoot">
      <div v-if="foot || slotFoot" :class="`footText ${footClass?footClass:''}`">
        <span v-if="foot && !slotFoot">{{foot}}</span>
        <slot name="foot" />
      </div>
      <component v-if="isLink" class="footArrow" :is="ArrowRight" />
    </div>
  </div>
  <div v-if="showBorder" :class="`listBorder ${icon || slotIcon?'':'listBorderNoIcon'}`"></div>
</template>
<script lang='ts' setup>
import { ref, useSlots, onMounted } from 'vue'
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
    default: false
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
  },
  iconClass: {
    type: String
  },
  titleClass: {
    type: String
  },
  descClass: {
    type: String
  },
  footClass: {
    type: String
  },
  itemClass: {
    type: String
  },
  disabled: {
    type: Boolean,
    default: false
  }
})
const touchstart = () => {
  if ((props.isLink || !!props.fun) && !props.disabled) {
    listItem.value.classList.add('itemTouch')
  }
}
const touchend = () => {
  listItem.value.classList.remove('itemTouch')
}
const clickList = () => {
  props.fun && !props.disabled && props.fun()
}
onMounted(() => {
  !props.isLink &&
    !props.fun &&
    listItem.value.classList.remove('listItemActive')
  props.disabled && listItem.value.classList.remove('listItemActive')
})
</script>
<style lang='sass' scoped>
.listItemBackgroundColor
  background-color: #ffffff
.listItem
  position: relative
  display: flex
  align-content: stretch
  padding: 15px 10px 15px 15px
  .maks
    position: absolute
    width: 100%
    background-color: #999999
    padding-bottom: 100%
    opacity: 0.5
    z-index: 1
    margin: -15px 0 0 -15px
  .listHead
    padding: 2px 10px 0 0
    .icon
      color: #999999
      width: 20px!important
      height: 20px!important
  .listBody
    flex: 1
    .listTitle
      font-size: 18px
    .listDesc
      font-size: 14px
      color: #999999
  .listFoot
    display: flex
    align-items: center
    .footText
      font-size: 14px
      color: #999999
      margin-right: 5px
    .footArrow
      width: 20px
      height: 20px
      color: #dddddd
.itemTouch
  background-color: rgba(220, 220, 220, 0.4)!important
.listItemActive:active
  background-color: rgba(220, 220, 220, 0.4)!important
.listBorder
  height: 0px
  border-top: 1px solid #dddddd
  transform: scaleY(.5)
  margin-left: 45px
.listBorderNoIcon
  margin-left: 15px
</style>
