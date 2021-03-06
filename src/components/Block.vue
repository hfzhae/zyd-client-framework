<template>
  <div class="blockItem">
    <div
      ref="blockBody"
      @touchstart="touchstart()"
      @touchend="touchend()"
      @click="clickblock"
      :class="`blockBody blockBodyActive ${itemClass?itemClass:'blockItemBackgroundColor'}`"
    >
      <div
        v-if="disabled"
        :class="`mask ${maskClass?maskClass:'maskBackgroundColor'}`"
        @click.stop="()=>{}"
      ></div>
      <div style="flex:1">
        <div class="blockIcon" v-if="icon || slotIcon">
          <component :class="iconClass?iconClass:''" v-if="icon && !slotIcon" :is="icon" />
          <slot name="icon"></slot>
        </div>
        <div :class="`blockTitle ${titleClass?titleClass:''}`" v-if="title || slotTitle">
          <span v-if="title && !slotTitle">{{title}}</span>
          <slot name="title"></slot>
        </div>
        <div :class="`blockDesc ${descClass?descClass:''}`" v-if="desc || slotDesc">
          <span v-if="desc && !slotDesc">{{desc}}</span>
          <slot name="desc"></slot>
        </div>
      </div>
      <div :class="`blockFoot ${footClass?footClass:''}`" v-if="foot || slotFoot">
        <span v-if="foot && !slotFoot">{{foot}}</span>
        <slot name="foot"></slot>
      </div>
    </div>
  </div>
</template>
<script lang='ts' setup>
import { ref, useSlots, onMounted } from 'vue'
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
  icon: {
    type: Object
  },
  fun: {
    type: Function
  },
  disabled: {
    type: Boolean,
    default: false
  },
  itemClass: {
    type: String
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
  disabled: {
    type: Boolean,
    default: false
  },
  maskClass: {
    type: String
  }
})
const slotIcon = !!useSlots().icon
const slotTitle = !!useSlots().title
const slotDesc = !!useSlots().desc
const slotFoot = !!useSlots().foot
const blockBody = ref(null)
const touchstart = () => {
  if (!props.disabled) {
    blockBody.value.classList.add('itemTouch')
  }
}
const touchend = () => {
  blockBody.value.classList.remove('itemTouch')
}
const clickblock = () => {
  props.fun && !props.disabled && !props.disabled && props.fun()
}
onMounted(() => {
  !props.fun && blockBody.value.classList.remove('blockBodyActive')
  props.disabled && blockBody.value.classList.remove('blockBodyActive')
})
</script>
<style lang='sass' scoped>
.blockItem
  width: 50%
  display: flex
  align-items: stretch
  .mask
    position: absolute
    width: 100%
    padding-bottom: 100%
    opacity: 0.8
    z-index: 1
    margin: -35px 0 0 -15px
  .maskBackgroundColor
    background-color: #ffffff
  .blockItemBackgroundColor
    background-color: #ffffff
  .blockBody
    overflow: hidden
    position: relative
    width: 100%
    border-radius: 10px
    margin-bottom: 10px
    margin-right: 5px
    padding: 15px
    display: flex
    .blockTitle
      font-size: 18px
      flex: 1
    .blockFoot
      font-size: 25px
      color: #999999
    .blockIcon
      .icon
        width: 25px!important
        height: 25px!important
        margin-right: 10px
        color: #999999
    .blockDesc
      font-size: 14px
      color: #999999
.itemTouch
  background-color: rgba(220, 220, 220, 0.4)!important
.blockBodyActive:active
  background-color: rgba(220, 220, 220, 0.4)!important
</style>