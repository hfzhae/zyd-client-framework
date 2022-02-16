<template>
  <div class="blockItem">
    <div
      ref="blockBody"
      @touchstart="touchstart()"
      @touchend="touchend()"
      @click="clickblock"
      :class="`blockBody ${itemClass?itemClass:'blockItemBackgroundColor'}`"
    >
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
import { ref, useSlots } from 'vue'
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
  }
})
const slotIcon = !!useSlots().icon
const slotTitle = !!useSlots().title
const slotDesc = !!useSlots().desc
const slotFoot = !!useSlots().foot
const blockBody = ref(null)
const touchstart = () => {
  blockBody.value.classList.add('itemTouch')
}
const touchend = () => {
  blockBody.value.classList.remove('itemTouch')
}
const clickblock = () => {
  props.fun && !props.disabled && props.fun()
}
</script>
<style lang='sass' scoped>
.blockItem
  width: 50%
  display: flex
  align-items: stretch
  .blockItemBackgroundColor
    background-color: #ffffff
  .blockBody
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
.blockBody:active
  background-color: rgba(220, 220, 220, 0.4)!important
</style>