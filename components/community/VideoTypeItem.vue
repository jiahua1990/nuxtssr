<template>
  <div>
    <div class="home-list-content">
      <div v-if="itemData.hasOwnProperty('description')">
        {{itemData.description}}
      </div>
      <div>
        <video v-show="isPlay" id="videos" class="video_preview" height="400" width="600" :src="videoSrc"
               controls="controls">
          您的浏览器不支持播放，建议换一个最新的浏览器!
        </video>
        <div class="video_cover" v-show="!isPlay" @click="play()">
          <img style="height: 400px;width: 600px;" class="bk-img" :src="avatar"/>
          <i class="video_playing iconfont icon-bofang"></i>
        </div>
      </div>
    </div>
    <div class="home-list-list">
      <div v-if="itemData.hasOwnProperty('tags') && itemData.tags.length>0" class="home-list-list-left">
        <a v-for="tag in itemData.tags" :key="tag.id" href="#">{{tag.name}}</a>
      </div>
      <div class="home-list-list-right">
        <span class="list-time">{{itemData.published_at | timeLL}}</span>
        <span><i class="iconfont icon-chakan"></i>{{itemData.read_num}}</span>
        <span><i class="iconfont icon-pinglun"></i>{{itemData.comment_num}}</span>
        <span><i class="iconfont icon-shoucang"></i>{{itemData.collect_num}}</span>
      </div>
    </div>
  </div>
</template>

<script>
  import typeMixin from './articleTypeItemMix'

  export default {
    mixins: [typeMixin],
    name: 'video-type-item',
    data () {
      return {
        isPlay: false
      }
    },
    mounted () {
      // this.$set(this.itemData, 'video_list', 'https://p-events-delivery.akamaized.net/17oiubaewrvouhboiubasdfv09/vod3/1709jbiuygwdfiug.mp4')
    },
    computed: {
      avatar () {
        return this.itemData.hasOwnProperty('image_list') ? this.itemData.image_list : this.itemData.avatar
      },
      videoSrc () {
        return 'https://p-events-delivery.akamaized.net/17oiubaewrvouhboiubasdfv09/vod3/1709jbiuygwdfiug.mp4'
      }
    },
    created () {
      console.log(this.itemData)
    },
    methods: {
      //点击播放视频
      play () {
        this.isPlay = true
        let videos = document.getElementById('videos')
        videos.play()
      }
    }
  }
</script>

<style scoped>

</style>
