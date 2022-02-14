# [zyd-client-framework](https://github.com/hfzhae/zyd-client-framework)
<p>
  <a href="https://github.com/hfzhae/zyd-client-framework/blob/master/LICENSE"><img style="margin-right:5px;" src="https://img.shields.io/badge/license-MIT-grren.svg"></a>
  <img style="margin-right:5px;" src="https://img.shields.io/badge/vue-v3-blue.svg">
  <img style="margin-right:5px;" src="https://img.shields.io/badge/element-plus-orange.svg">
</p>

## Installation
```
$ npm install -s zyd-client-framework
```

## Import
>/index.js
```js
import { List, ListGroup } from 'zyd-client-framework'
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
<ListGroup title="title"></ListGroup>
```

## LeftSlider
```html
<ListGroup>
  <LeftSlider v-for="item in 10" :key="item">
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