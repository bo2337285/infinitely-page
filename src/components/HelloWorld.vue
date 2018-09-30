<template>
  <v-touch class="touch-content" @panstart="panstart" @panup="panup" @pandown="pandown" @panend="panend">
    <div class="page">
      <div class="img-wraper">
        <img class="img" :src="currImg" />
      </div>
      </div>
  </v-touch>
</template>

<script>
import img0 from '@/assets/img0.jpg'
import img1 from '@/assets/img1.jpg'
import re from '@/assets/re.jpg'
import re0 from '@/assets/re0.jpg'
export default {
  name: 'HelloWorld',
  data() {
    return {
      actionStatus: 0, // 0 normal, 1 panup, 2 pandown
      currImg: '',
      listIdx: 0,
      reFlag: false,
      normalList: [img0, img1],
      reList: [re, re0]
    }
  },
  created() {
    this.currImg = this.imgList[this.listIdx]
    // 预加载图片
    this.imgList.forEach(item => {
      let img = new Image()
      img.src = item
    });
  },
  watch: {
    listIdx() {
      if (!this.reFlag && this.listIdx > 1) { // 过完第一个normalList的图片后
        this.reFlag = true
        this.listIdx = 0
      }
      this.currImg = this.imgList[this.listIdx]
    }
  },
  computed: {
    imgList() {
      return this.reFlag ? this.reList : [...this.normalList, ...this.reList]
    },
  },
  methods: {
    panstart(params) {
    },
    panup(params) {
      this.actionStatus = 1
    },
    pandown(params) {
      this.actionStatus = 2
    },
    panend() {
      this.actionStatus == 1 ? this.next() : this.prev()
      this.actionStatus = 0
    },
    prev() {
      let idx = this.listIdx - 1
      if(this.reFlag){
        this.listIdx = idx < 0 ? this.imgList.length - 1 : idx
      }else{
        this.listIdx = idx < 0 ? 0 : idx
      }
      console.log(this.listIdx);
    },
    next() {
      let idx = this.listIdx + 1
      this.listIdx = idx > this.imgList.length - 1 ? 0 : idx
      console.log(this.listIdx);
    },
  }
}
</script>

<style lang="stylus" scoped>
.touch-content
  width 100%
  height 100%
  .page
    width 100%
    height 100%
    display flex
    justify-content center
    align-items center
    .img
      display inline-block
      width 100%
</style>
