<template>
  <div class="listGroupTitle" v-if="title">{{title}}</div>
  <div
    :class="`listGroupItem ${itemClass?itemClass:'listGroupItemBackgroundColor'}`"
    :style="groupStyle?groupStyle:''"
  >
    <div v-if="disabled" class="maks"></div>
    <slot />
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
  }
})
</script>
<style lang='sass' scoped>
.listGroupItemBackgroundColor
  background-color: #ffffff
.listGroupItem
  position: relative
  overflow: hidden
  margin: 20px
  padding: 0 0 0 0
  border-radius: 10px
  :deep(.listBorder:last-child)
    display: none
  .maks
    position: absolute
    width: 100%
    background-color: #999999
    padding-bottom: 100%
    opacity: 0.5
    z-index: 1
.listGroupTitle
  margin: 20px 0 -15px 25px
  font-size: 18px
  color: #000000
</style>
