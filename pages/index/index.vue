<script setup lang="ts">
const { data: channelList } = await useFetch('/api/channelget')
const { data: videoList } = await useFetch('/api/video')
import type { videoItem } from '@/types/video'

const list = ref<videoItem[]>([])
const loading = ref(false)
const finished = ref(false)
let page = 1
let pageSize = 20
const onLoad = () => {
  loading.value = false
  const data = videoList.value?.slice(
    (page - 1) * pageSize,
    page * pageSize,
  ) as videoItem[]
  list.value.push(...data)
  page++
  if (videoList.value?.length === list.value.length) {
    finished.value = true
  }
}
onLoad()
</script>

<template>
  <AppHeader />
  <!-- 频道模块 -->
  <van-tabs>
    <van-tab v-for="item in channelList" :key="item.id" :title="item.name" />
  </van-tabs>
  <van-list
    v-model:loading="loading"
    :finished="finished"
    finished-text="没有更多了"
    @load="onLoad"
  >
    <!-- 视频列表 -->
    <div class="video-list">
      <AppVideo v-for="item in list" :key="item.bvid" :item="item" />
    </div>
  </van-list>
</template>

<style lang="scss">
// 公共头部
.app-header {
  display: flex;
  align-items: center;
  padding: 8px 12px;
  background-color: #fff;
  .logo {
    flex: 1;
    .Navbar_logo {
      color: #fb7299;
      font-size: 28px;
    }
  }
  .search {
    padding: 0 8px;
    .ic_search_tab {
      color: #ccc;
      font-size: 22px;
    }
  }
  .face {
    padding: 0 15px;
    img {
      width: 24px;
      height: 24px;
    }
  }
  .down-app {
    font-size: 12px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #fb7299;
    color: #fff;
    border-radius: 5px;
    padding: 5px 10px;
  }
}

// 视频列表
.video-list {
  display: flex;
  flex-wrap: wrap;
  padding: 10px 5px;
}
</style>
