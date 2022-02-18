# [zyd-client-framework](https://github.com/hfzhae/zyd-client-framework)
<p>
  <a href="https://github.com/hfzhae/zyd-client-framework/blob/master/LICENSE"><img style="margin-right:5px;" src="https://img.shields.io/badge/license-MIT-grren.svg"></a>
  <img style="margin-right:5px;" src="https://img.shields.io/badge/vue-3.x-blue.svg">
  <img style="margin-right:5px;" src="https://img.shields.io/badge/elementUI-plus-orange.svg">
</p>

## Installation
```
$ npm install -s zyd-client-framework
```

## Import
```js
import { List, ListGroup, LeftSlider, Block, BlockGroup } from 'zyd-client-framework'
```

## List
#### property
name|explain|type|default|examples
-|-|-|-|-
title|标题|String||title="标题"
desc|副标题|String||desc="副标题"
foot|右侧副标题|String||foot="145"
isLink|是否显示右侧剪头|Boolean|false|:isLink="false"
fun|点击事件调用的方法|Function||:fun="getItem"
icon|图标对象，同elementUI Plus的icon使用方法|Object||:icon="plus"
showBorder|是否显示行间边框|Boolean|true|:showBorder="false"
disabled|是否禁用|Boolean|false|:disabled="true"
iconClass|图标css类名|String||iconClass="iconClass"
titleClass|标题css类名|String||titleClass="titleClass"
descClass|副标题css类名|String||descClass="descClass"
footClass|右侧副标题css类名|String||footClass="footClass"
itemClass|List元素css类名|String||itemClass="itemClass"
maskClass|禁用遮罩层css类名|String||maskClass="maskClass"
#### examples
```html
<List
  title="title"
  desc="desc"
  foot="foot"
  :isLink="true"
  :fun="()=>{}"
  :icon="IceCreamRound"
  :showBorder="true"
  :disabled="true"
  iconClass="iconClass"
  titleClass="titleClass"
  descClass="descClass"
  footClass="footClass"
  itemClass="itemClass"
  maskClass="maskClass"
></List>
```
#### Slot
name|explain
-|-
icon|图标插槽
title|标题插槽
desc|副标题插槽
foot|右侧副标题插槽
#### examples
```html
<List>
  <template #icon>
    <component class="listIcon" :is="icon" />
  </template>
  <template #title>title</template>
  <template #desc>desc</template>
  <template #foot>foot</template>
</List>
```

## ListGroup
#### property
name|explain|type|default|examples
-|-|-|-|-
title|标题|String||title="标题"
disabled|是否禁用|Boolean|false|:disabled="true"
titleClass|标题css类名|String||titleClass="titleClass"
maskClass|禁用遮罩层css类名|String||maskClass="maskClass"
#### examples
```html
<ListGroup 
  :disabled="true" 
  maskClass="maskClass" 
  itemClass="itemClass" 
  title="title"
>
  <List />
</ListGroup>
```

## Block
#### property
name|explain|type|default|examples
-|-|-|-|-
title|标题|String||title="标题"
desc|副标题|String||desc="副标题"
foot|右侧副标题|String||foot="145"
fun|点击事件调用的方法|Function||:fun="getItem"
icon|图标对象，同elementUI Plus的icon使用方法|Object||:icon="plus"
showBorder|是否显示行间边框|Boolean|true|:showBorder="false"
disabled|是否禁用|Boolean|false|:disabled="true"
iconClass|图标css类名|String||iconClass="iconClass"
titleClass|标题css类名|String||titleClass="titleClass"
descClass|副标题css类名|String||descClass="descClass"
footClass|右侧副标题css类名|String||footClass="footClass"
itemClass|List元素css类名|String||itemClass="itemClass"
maskClass|禁用遮罩层css类名|String||maskClass="maskClass"
#### examples
```html
<Block
  title="title"
  desc="desc"
  foot="foot"
  :icon="IceCreamRound"
  :showBorder="true"
  :fun="()=>{}"
  :disabled="true"
  iconClass="iconClass"
  titleClass="titleClass"
  descClass="descClass"
  footClass="footClass"
  itemClass="itemClass"
  maskClass="maskClass" 
/>
```
#### slot
name|explain
-|-
icon|图标插槽
title|标题插槽
desc|副标题插槽
foot|右侧副标题插槽
#### examples
```html
<Block>
  <template #icon>
    <component class="blockIcon" :is="icon" />
  </template>
  <template #title>title</template>
  <template #desc>desc</template>
  <template #foot>foot</template>
</Block>
```

## BlockGroup
#### property
name|explain|type|default|examples
-|-|-|-|-
title|标题|String||title="标题"
disabled|是否禁用|Boolean|false|:disabled="true"
#### examples
```html
<BlockGroup groupStyle="margin:0px;" groupClass="groupClass" :disabled="true" title="title">
  <Block />
</BlockGroup>
```
## LeftSlider
#### property
name|explain|type|default|examples
-|-|-|-|-
itemClass|List元素css类名|String||itemClass="itemClass"
menuClass|右侧按钮菜单css类名|String||menuClass="menuClass"
showBorder|是否显示行间边框|Boolean|true|:showBorder="false"
transition|滑块动画时长|Number|0.3|:transition="0.1"

```html
<ListGroup>
  <LeftSlider 
    v-for="item in 10"
    :key="item"
    :showBorder="true"
    :transition="0.3"
    itemClass="itemClass"
    menuClass="menuClass"
  >
    <List desc="desc" foot="foot" isLink :fun="()=>{}" :icon="IceCreamRound">
      <template #title>title{{item}}</template>
    </List>
    <template #rightMenu>
      <div style="margin: 0 20px">del</div>
    </template>
  </LeftSlider>
</ListGroup>
```
#### slot
name|explain
-|-
rightMenu|右侧按钮菜单插槽
#### examples
```html
<template #rightMenu>
  <div style="margin: 0 20px">del</div>
</template>
```
