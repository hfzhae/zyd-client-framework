# [zyd-client-framework](https://github.com/hfzhae/zyd-client-framework)
<p>
  <a href="https://github.com/hfzhae/zyd-client-framework/blob/master/LICENSE"><img style="margin-right:5px;" src="https://img.shields.io/badge/license-MIT-grren.svg"></a>
  <img style="margin-right:5px;" src="https://img.shields.io/badge/vue-3.x-blue.svg">
  <img style="margin-right:5px;" src="https://img.shields.io/badge/element-plus-orange.svg">
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
```html
<BlockGroup groupClass="groupClass" title="title">
  <Block />
</BlockGroup>
```

## LeftSlider
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
```html
<template #rightMenu>
  <div style="margin: 0 20px">del</div>
</template>
```
