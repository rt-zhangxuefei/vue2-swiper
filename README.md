# vue2-slider

> it is a usefull slider component based on vue 2.x<br/>基于vue2.x实现的一个焦点图组件，提供基本的自动播放，点击跳转，无限循环滑动功能

# 立即使用（How to use)
> 引入src/components/slider.vue组件<br/>
> 如果没有链接，则不需要嵌套a标签
```html
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
or need not any link
```html
<template>
  <div>
    <slider>
      <div v-for="(item,index) in data" :key="index">
          <img :src="item.picUrl"></img>
      </div>
    </slider>
  </div>
</template>
```

# 参数（Options）
```javascript
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
