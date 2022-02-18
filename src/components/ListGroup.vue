<template>
  <div class="listGroup" :style="groupStyle?groupStyle:''">
    <div class="listGroupTitle" v-if="title">{{title}}</div>
    <div :class="`listGroupItem ${itemClass?itemClass:'listGroupItemBackgroundColor'}`">
      <div v-if="disabled" :class="`mask ${maskClass?maskClass:'maskBackgroundColor'}`"></div>
      <slot />
    </div>
  </div>
</template>
<script lang='ts' setup>
const props = defineProps({
  title: {
    type: String,
    default: ''
  },
  groupStyle: {
    type: String
  },
  itemClass: {
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
</script>
<style lang='sass' scoped>
.listGroupItemBackgroundColor
  background-color: #ffffff
.listGroup
  margin: 20px
.listGroupItem
  position: relative
  overflow: hidden
  padding: 0 0 0 0
  border-radius: 10px
  :deep(.listBorder:last-child)
    display: none
  .mask
    position: absolute
    width: 100%
    padding-bottom: 100%
    opacity: 0.8
    z-index: 1
    margin: -20px 0 0 0
  .maskBackgroundColor
    background-color: #ffffff
.listGroupTitle
  margin: 0 0 5px 10px
  font-size: 16px
</style>