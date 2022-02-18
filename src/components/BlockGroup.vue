<template>
  <div class="blockGroup" :style="groupStyle?groupStyle:''">
    <div class="blockGroupTitle" v-if="title">{{title}}</div>
    <div class="blockGroupItem">
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
  groupClass: {
    type: String
  },
  disabled: {
    type: Boolean,
    default: false
  },
  groupStyle: {
    type: String
  }
})
</script>
<style lang='sass' scoped>
.blockGroup
  margin: 20px
.blockGroupItem
  overflow: hidden
  display: flex
  flex-wrap: wrap
  border-radius: 10px
.blockGroupTitle
  margin: 0 0 5px 10px
  font-size: 16px
</style>