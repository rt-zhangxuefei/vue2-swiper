<template>
  <div id="app">
    <slider>
      <div v-for="(item,index) in recommends" :key="index">
        <a :href="item.linkUrl">
          <img :src="item.picUrl"></img>
        </a>
      </div>
    </slider>
  </div>
</template>

<script>
import Slider from './components/Slider'

export default {
  name: 'app',
  data() {
    return {
      recommends: [
        {
          'linkUrl': 'https://y.qq.com/m/digitalbum/gold/index.html?_video=true&id=2185201&g_f=shoujijiaodian',
          'picUrl': 'http://y.gtimg.cn/music/photo_new/T003R720x288M000003KrRKE3oyCGn.jpg',
          'id': 11154
        },
        {
          'linkUrl': 'https://y.qq.com/msa/264/0_3845.html',
          'picUrl': 'http://y.gtimg.cn/music/photo_new/T003R720x288M000001VvJxH1ynxty.jpg',
          'id': 11123
        },
        {
          'linkUrl': 'http://y.qq.com/w/album.html?albummid=003lJcXW0xXDBI',
          'picUrl': 'http://y.gtimg.cn/music/photo_new/T003R720x288M000000ucX331KWjTV.jpg',
          'id': 11185
        },
        {
          'linkUrl': 'https://y.qq.com/m/digitalbum/gold/index.html?_video=true&id=2167319&g_f=shoujijiaodian',
          'picUrl': 'http://y.gtimg.cn/music/photo_new/T003R720x288M000001yN6bj1IeGTi.jpg',
          'id': 11151
        },
        {
          'linkUrl': 'http://y.qq.com/w/taoge.html?id=0',
          'picUrl': 'http://y.gtimg.cn/music/photo_new/T003R720x288M000004G9Tbm3Y1RbT.jpg',
          'id': 11166
        }
      ]
    }
  },
  components: {
    Slider
  }
}
</script>

<style lang="stylus">
  *
    margin:0
    padding:0
</style>

