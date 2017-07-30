# vue2-slider

> it is a usefull slider component based on vue2

# 立即使用（How to use)
```
<template>
  <div>
    <slider>
      <div v-for="(item,index) in data" :key="index">
        <a :href="item.linkUrl">
          <img :src="item.picUrl"></img>
        </a>
      </div>
    </slider>
  </div>
</template>
```
# 参数（Options）
```
  props: {
    loop: {
      type: Boolean,
      default: true
    },
    autoPlay: {
      type: Boolean,
      default: true
    },
    interval: {
      type: Number,
      default: 4000
    },
    speed: {
      type: Number,
      default: 500
    }
  }
```
